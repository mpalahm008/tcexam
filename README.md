Persyaratan sistem
Petunjuk instalasi mengasumsikan bahwa Anda memiliki server web yang berfungsi penuh.

Ini adalah persyaratan minimum yang diperlukan sebelum instalasi TCExam berhasil:
•	Server Web: Apache 1.3+ ( http://httpd.apache.org/ ) atau IIS 6+ ( http://www.microsoft.com ).
•	PHP 5.5+ ( http://www.php.net )
Anda harus memastikan bahwa Anda telah mengaktifkan pustaka gd , imagick , curl , mysql , dan pgsql dalam instalasi PHP Anda.
•	DMBS : MySQL 4.1+ ( http://www.mysql.com ) atau PostgreSQL 8.2+ ( http://www.postgresql.org )
•	Rendering LaTeX memerlukan perangkat lunak tambahan berikut :
o	LaTeX ( http://www.latex-project.org/ ), untuk Windows saya sarankan menggunakan MiKTeX ( http://miktex.org/ );
o	GambarMagick ( http://www.imagemagick.org/ );
o	Skrip hantu ( http://sourceforge.net/projects/ghostscript/ ).
•	Sistem Pengenalan Tanda Optik (OMR) memerlukan aplikasi zbarimg ( http://zbar.sourceforge.net )
Untuk bantuan dalam instalasi dan konfigurasi server web dan perpustakaan yang diperlukan, silakan merujuk ke manual khusus.
Jika menginstal di komputer rumah atau kantor Anda (hanya untuk pengujian lokal) ada sejumlah paket untuk berbagai sistem operasi yang akan membantu dalam menetapkan persyaratan berikut:
•	XAMPP - Multi-platform - Apache, MySQL, PHP, instalasi. http://www.apachefriends.org/en/xampp.html .
•	WAMP - Platform Windows - Apache, MySQL, PHP, instalasi. http://www.wampserver.com/en/
•	MAMP - Platform Macintosh - Apache MySQL, PHP, instalasi. http://www.mamp.info/en/index.php
Jika Anda menggunakan OS Debian/Ubuntu, kami menyarankan untuk menginstal paket berikut:
•	Untuk MySQL:
sudo apt-get install acpid apache2 ghostscript gsfonts imagemagick libapache2-mod-auth-mysql libapache2-mod-auth-plain libapache2-mod-php5 libauthen-pam-perl libio-pty-perl libmd5-perl libnet-ssleay-perl libpam-runtime lm-sensors mysql-client mysql-server openssl perl php5 php5-cli php5-intl php5-gd php5-imagick php5-curl php5-mcrypt php5-memcache php5-mysql php5-xcache ssh tetex-base tetex-bin tetex-extra texlive-base-bin zbar-tools
•	Untuk PostgreSQL:
sudo apt-get install acpid apache2 ghostscript gsfonts imagemagick libapache2-mod-auth-pgsql libapache2-mod-auth-plain libapache2-mod-php5 libauthen-pam-perl libio-pty-perl libmd5-perl libnet-ssleay-perl libpam-runtime lm-sensors openssl perl php5 php5-cli php5-intl php5-gd php5-imagick php5-curl php5-mcrypt php5-memcache php5-pgsql php5-xcache postgresql postgresql-client postgresql-contrib ssh tetex-base tetex-bin tetex-extra texlive-base-bin zbar-tools
Pada server jarak jauh, yang dihosting, atau khusus, konfigurasi dan ketersediaan aplikasi ini akan bergantung pada penyedia host atau sistem operasi yang diinstal pada server. Jika Anda mengalami masalah dengan penyedia host Anda dan penggunaan TCExam, periksa halaman dukungan dan layanan .
Konfigurasi DBMS
Agar TCExam berfungsi dengan baik, Anda harus memiliki MySQL atau Database PostgreSQL yang berfungsi sebelum memulai proses instalasi.
TCExam akan membuat database dan tabel terkait, asalkan rinciannya dimasukkan dengan benar, selama proses instalasi. Namun terkadang, database mungkin perlu dibuat terlebih dahulu. Catat saja pengaturan yang sesuai sebelum melanjutkan instalasi:
•	Nama database MySQL/PostgreSQL Anda. Ini mungkin sudah diatur sebelumnya pada beberapa pengaturan server yang dihosting.
•	Nama host MySQL/PostgreSQL. Ini biasanya disebut "localhost" jika Anda menginstal di PC atau server lokal. Namun, jika Anda menggunakan shared hosting, tanyakan kepada penyedia hosting Anda untuk memastikan hal ini.
•	Nama pengguna MySQL/PostgreSQL. Ini mungkin telah dialokasikan oleh penyedia server Anda. Instalasi MySQL lokal umumnya memiliki nama pengguna administrator default yang ditetapkan sebagai "root".
•	Kata sandi MySQL/PostgreSQL. Ini mungkin telah dialokasikan oleh penyedia server Anda. Instalasi MySQL lokal umumnya memiliki kata sandi administrator default yang disetel ke kolom kosong. TCExam selalu memerlukan kata sandi yang tidak kosong. Untuk mengubah kata sandi gunakan sintaks berikut:
•	[MySQL]
•	mysql - kamu melakukan root
•	PERBARUI mysql.user SET Kata Sandi=PASSWORD('kata sandi saya') WHERE Pengguna='root';
•	HAK ISTIMEWA PENYIMPANAN;
•	berhenti;
•	[PostgreSQL]
•	sudo su postgres -c templat psql 1
•	ALTER USER postgres DENGAN PASSWORD 'mypassword';
Q
Konfigurasi PHP
Untuk penggunaan TCExam yang benar, PHP harus dikonfigurasi untuk mendukung sistem dan perpustakaan yang ditunjukkan di atas.
Beberapa parameter PHP juga harus diatur sebagai berikut:
•	php.ini
•	date.timezone = Eropa/Roma ; http://php.net/manual/en/timezones.php
•	arg_separator.output = “&”
•	magic_quotes_gpc = Aktif
•	magic_quotes_runtime = Mati
•	magic_quotes_sybase = Mati
permintaan_pesanan = “GPC”
•	Modul Apache ( /etc/httpd/conf/httpd.conf ):
•	TambahkanDefaultCharset UTF-8
•	php_value arg_separator.output "&"
•	php_value magic_quotes_gpc Aktif
•	php_value magic_quotes_runtime Mati
•	php_value magic_quotes_sybase Mati
php_nilai permintaan_pesanan "GPC"
Instalasi
Saat memasang TCExam untuk pertama kalinya, verifikasi persyaratan sistem . Dengan asumsi Anda memiliki server web Apache/IIS yang berfungsi, dengan PHP dan DBMS MySQL/PostgreSQL, Anda sedang dalam proses menginstal TCExam.
Jika Anda mendapatkan kode sumber TCExam untuk pertama kalinya, harap ganti nama folder "config.default" di dalam admin, publik, dan dibagikan menjadi "config".
Peningkatan TCExam
Proses peningkatan TCExam mungkin berbeda pada setiap rilis. Instruksi terperinci terdapat pada file UPGRADE.TXT yang dilampirkan pada setiap rilis TCExam.
Mendapatkan file
TCExam dapat diunduh dari GitHub . File tersebut adalah arsip terkompresi sehingga Anda memerlukan program utilitas, baik secara lokal atau di server host Anda, yang dapat "mengunzip" file tersebut (yaitu WinZip, WinRAR, 7Zip). Pastikan Anda memilih versi rilis stabil terbaru.
Menginstal File
Kami berasumsi Anda telah membuat server web yang berfungsi, dengan persyaratan yang diperlukan , dan Anda tahu di mana harus meletakkan file untuk ditampilkan di server web.
Buka zip file distribusi ke direktori di bawah root server web Anda. Jika Anda menggunakan server web Apache, ini biasanya c:apache groupapachehtdocs pada OS Windows dan /usr/local/apache/htdocs atau /var/www/ pada sistem mirip UNIX tetapi ini bervariasi terutama pada server yang dihosting dan antara distribusi OS GNU-Linux yang berbeda.
Apa yang Anda lakukan untuk menginstal TCExam pada host jarak jauh sangat bergantung pada fasilitas yang disediakan oleh host Anda - sehubungan dengan perangkat lunak Panel Kontrol dan sumber daya koneksi. Ini mungkin juga bergantung pada keahlian Anda mengenai metode akses server. Prosedur sederhana dan umum mungkin melibatkan: unzip file distribusi TCExam ke direktori lokal di komputer lokal Anda dan kemudian FTP file tersebut ke server host dan menempatkannya langsung di bawah, atau di, direktori di bawah root server web. Ada banyak program FTP gratis yang tersedia untuk operasi ini, seperti Filezilla. Pencarian Google atau kunjungan ke salah satu situs sumber daya terbuka akan membantu Anda menemukan alat yang sesuai.

Setelah Anda selesai mengunggah file dan folder, ubah pemilik file menjadi pengguna server Web (biasanya “www-data” atau “Apache”). Pada sistem berbasis POSIX (seperti Unix, Linux, dll), ubah ke direktori TCExam dan masukkan perintah sistem berikut (gantikan nama pengguna yang sesuai untuk sistem Anda): chown -R apache:apache /var/www/tcexam .
Ubah izin akses file sehingga semua pengguna dapat menulis ke dalamnya. Pada sistem berbasis POSIX, ubah ke direktori TCExam dan masukkan perintah sistem berikut: chmod -R 777 /var/www/tcexam . Untuk alasan keamanan, Anda harus mengatur izin file-file ini dengan benar di akhir proses instalasi.
Instalasi Peramban
Jenis instalasi ini akan secara otomatis menginstal database dan mengkonfigurasi parameter sistem yang penting. Proses instalasi akan menghapus semua data instalasi TCExam sebelumnya, itulah sebabnya dalam hal ini disarankan untuk membuat salinan cadangan data tersebut.

Arahkan browser Web Anda (yaitu Mozilla Firefox atau Internet Explorer) ke skrip instalasi TCExam (http://www.yoursite.com/install/install.php atau http://yoursite.com/tcexam_folder/install/install.php) . Untuk memulai instalasi Anda harus mengisi formulir dengan lengkap dan tekan tombol INSTALL.
Bidang yang wajib diisi adalah:
•	tipe db : tipe DBMS (defaultnya adalah MySQL ).
•	db host : nama host database (biasanya localhost ).
•	port db : port database (biasanya 3306 untuk MySQL atau 5432 untuk PostgreSQL).
•	db user : nama pengguna database (biasanya root untuk MySQL dan postgres untuk PostgreSQL).
•	db password : kata sandi pengguna untuk mengakses database.
•	nama db : nama database (biasanya TCExam). Nama ini harus diubah ketika ada salinan TCExam lain di sistem yang sama.
•	awalan tabel : awalan yang akan ditambahkan ke nama tabel (biasanya tce_ ).
•	URL host : nama domain situs Anda (yaitu http://www.situsAnda.com atau https://www.situsAnda.com ).
•	URL relatif : jalur relatif dari root server web Anda tempat file TCExam berada (biasanya / atau /tcexam_folder/).
•	Jalur TCExam : jalur lengkap folder tempat TCExam diinstal (yaitu /usr/local/Apache/htdocs/TCExam/ atau c:/Inetpub/wwwroot/TCExam/ ).
•	Port TCExam : port koneksi default (biasanya 80 untuk HTTP atau 443 untuk SSL - HTTPS).
Jika instalasi berhasil diselesaikan, sistem siap untuk eksekusi pertama. Pada titik ini Anda dapat melompat ke bagian Pasca Instalasi dan Konfigurasi .
Jika instalasi tidak berhasil diselesaikan, Anda dapat menggunakan prosedur manual yang dijelaskan di bagian selanjutnya.
Instalasi Manual
Untuk menginstal TCExam secara manual, Anda harus mengedit beberapa file konfigurasi dan menginstal database.

File penting dan parameter konfigurasi adalah:
•	dibagikan/config/cp_db_config.php
o	K_DATABASE_TYPE (tipe database, biasanya MYSQL atau POSTGRESQL )
o	K_DATABASE_HOST (nama host database, biasanya localhost )
o	K_DATABASE_NAME (nama database, biasanya TCExam )
o	K_DATABASE_USER_NAME (nama pengguna database, biasanya root )
o	K_DATABASE_USER_PASSWORD (kata sandi untuk mengakses database)
o	K_TABLE_PREFIX (awalan yang akan ditambahkan pada nama tabel, biasanya tce_ )
•	dibagikan/config/cp_paths.php
o	K_PATH_HOST (nama domain situs Anda, yaitu http://www.yoursite.com )
o	K_PATH_TCEXAM (jalur relatif dari root server web Anda tempat file TCExam berada, biasanya / atau /tcexam_folder/)
o	K_PATH_MAIN (path lengkap ke folder tempat TCExam diinstal, yaitu /usr/local/apache/htdocs/TCExam/ atau c:/Inetpub/wwwroot/TCExam/ )
o	K_STANDARD_PORT (port komunikasi http, biasanya 80 atau 443 untuk SSL)
Instalasi Basis Data
Di folder instalasi ada semua file SQL dengan struktur dan data database:
•	mysql_db_structure.sql - Berisi struktur database MySQL.
•	pgsql_db_structure.sql - Berisi struktur database PostgreSQL.
•	db_data.sql - Berisi data database default.
Jika Anda ingin mengubah awalan tabel Anda harus menggunakan editor teks dengan fungsi pencarian dan penggantian dan melakukan substitusi berikut:
•	Pada file ..._db_structure.sql gantikan CREATE TABLE tce_ dengan CREATE TABLE awalan Anda
•	Pada file db_data.sql gantikan INSERT INTO tce_ dengan INSERT INTO yourprefix
Untuk mengeksekusi file SQL Anda dapat menggunakan perintah DBMS dari command shell server. Untuk MySQL Anda dapat menggunakan sintaks berikut:
mysql -u root -p
mysql> BUAT DATABASE TCExam;
mysql> keluar
cangkang> mysql -u root -p TCExam < mysql_db_structure.sql
cangkang> mysql -u root -p TCExam < db_data.sql
Sebagai pilihan lain Anda dapat menggunakan manajer DBMS eksternal (yaitu phpMyAdmin, phpPgAdmin, pgAdmin3, dll.) untuk membuat database dan menjalankan file SQL dengan menggunakan perintah khusus.
Pasca Instalasi dan Konfigurasi
Setelah instalasi selesai, Anda harus:
•	hapus folder instalasi karena tidak diperlukan lagi dan mewakili masalah keamanan sistem ( rm -fR /var/www/tcexam/install );
•	ada perintah tambahan yang diperlukan untuk memastikan bahwa file tidak dapat diubah kecuali dimaksudkan oleh administrator; pada sistem POSIX Anda dapat menggunakan perintah berikut:
cd /var/www/tcexam
find . -exec chown -R apache:apache {} \;
find . -type f -exec chmod 544 {} \;
find cache/ -type f -exec chmod 644 {} ;
find cache/lang -type f -exec chmod 544 {} \;
find admin/backup -type f -exec chmod 644 {} \;
find admin/log/ -type f -exec chmod 644 {} \;
find public/log/ -type f -exec chmod 644 {} \;
find . -type d -exec chmod 755 {} ;
(dalam contoh ini /var/www/tcexam adalah folder instalasi, apache adalah nama pengguna dan grup Apache)
•	konfigurasikan TCExam agar sesuai dengan kebutuhan Anda dan aktifkan fitur tambahan.
Konfigurasi
Setelah prosedur instalasi di atas berhasil diselesaikan, TCExam akan bekerja dalam mode "dasar". Beberapa langkah konfigurasi tambahan diperlukan untuk mengaktifkan beberapa fitur (RADIUS, email, LaTeX) dan untuk mempersonalisasi beberapa pengaturan agar sesuai dengan kebutuhan Anda. Yang harus Anda lakukan adalah mengedit file konfigurasi berikut secara manual:
•	shared/config/ - File konfigurasi utama:
o	lang/ - file bahasa
	bahasa_tmx.xml - File bahasa TMX (berisi semua terjemahan)
o	tce_cas.php - File konfigurasi untuk CAS (Layanan Otentikasi Pusat)
o	tce_config.php - konfigurasi umum sistem
o	tce_db_config.php - konfigurasi basis data
o	tce_email_config.php - konfigurasi umum sistem email
o	tce_general_constants.php - konstanta umum
o	tce_latex.php - Konfigurasi LaTeX
o	tce_ldap.php - Konfigurasi LDAP
o	tce_mime.php - Asosiasi MIME ke ekstensi file
o	tce_paths.php - jalur file dan folder dalam sistem
o	tce_pdf.php - konfigurasi format dan header dokumen PDF
o	tce_radius.php - Konfigurasi RADIUS
o	tce_user_registration.php - konfigurasi pendaftaran pengguna
•	admin/config/ - File konfigurasi untuk area administrasi:
o	tce_auth.php - konfigurasi tingkat akses untuk modul administrasi
o	tce_config.php - konfigurasi umum untuk panel administrasi
•	public/config/ - File konfigurasi untuk area publik:
o	tce_auth.php - konfigurasi tingkat akses untuk modul publik
o	tce_config.php - konfigurasi umum untuk area publik
File konfigurasi sudah cukup jelas. Jika Anda mengalami masalah silakan periksa halaman Dukungan dan Layanan .
Akses dan Keamanan
Setelah prosedur instalasi dan konfigurasi selesai, Anda dapat mengakses bagian administrasi dengan mengarahkan browser Web Anda ke http://www.yoursite.com/tcexam_folder/admin/code/ dan menggunakan nama pengguna dan kata sandi berikut:
•	nama: admin
•	kata sandi: 1234
Untuk melindungi sistem Anda dan diberikan akses pribadi yang unik, ingatlah untuk mengubah kata sandi dengan formulir Pengguna .

Untuk mencapai tingkat keamanan yang lebih baik Anda harus melindungi seluruh folder admin dengan sistem autentikasi pengguna berbasis web. Untuk Apache, periksa Otentikasi, Otorisasi, dan Kontrol Akses Apache .
Harap lindungi secara terpisah folder admin/backup em> atau pindahkan folder cadangan ke lokasi lain yang dilindungi dan atur konstanta K_PATH_BACKUP di shared/config/tce_paths.php . Isi direktori ini tidak boleh tersedia melalui browser Web.

