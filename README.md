System Requirements
The installation instructions assumes that you have a fully functioning web server.

These are the minimum requirements needed before installation of TCExam can be successful:

A Web server: Apache 1.3+ (http://httpd.apache.org/) or IIS 6+ (http://www.microsoft.com).
PHP 5.5+ (http://www.php.net)
You must ensure that you have gd, imagick, curl, mysql, and pgsql libraries enabled within your PHP installation.
A DMBS:MySQL 4.1+ (http://www.mysql.com) or PostgreSQL 8.2+ (http://www.postgresql.org)
The LaTeX rendering requires the following additional software:
LaTeX (http://www.latex-project.org/), for Windows I suggest to use MiKTeX (http://miktex.org/);
ImageMagick (http://www.imagemagick.org/);
Ghostscript (http://sourceforge.net/projects/ghostscript/).
The Optical Mark Recognition (OMR) system requires zbarimg application (http://zbar.sourceforge.net)
For help with the installation and configuration of the web server and the required libraries please refer to the specific manuals.
If installing on your home or office computer (for local testing only) there are a number of packages for the various operating systems that will assist in establishing these requirements:

XAMPP - Multi-platform - Apache, MySQL, PHP, installation. http://www.apachefriends.org/en/xampp.html.
WAMP - Windows platform - Apache, MySQL, PHP, installation. http://www.wampserver.com/en/
MAMP - Macintosh platform - Apache MySQL, PHP, installation. http://www.mamp.info/en/index.php
If you are using a Debian/Ubuntu OS, we suggest to install the following packages:

For MySQL:
sudo apt-get install acpid apache2 ghostscript gsfonts imagemagick libapache2-mod-auth-mysql libapache2-mod-auth-plain libapache2-mod-php5 libauthen-pam-perl libio-pty-perl libmd5-perl libnet-ssleay-perl libpam-runtime lm-sensors mysql-client mysql-server openssl perl php5 php5-cli php5-intl php5-gd php5-imagick php5-curl php5-mcrypt php5-memcache php5-mysql php5-xcache ssh tetex-base tetex-bin tetex-extra texlive-base-bin zbar-tools

For PostgreSQL:
sudo apt-get install acpid apache2 ghostscript gsfonts imagemagick libapache2-mod-auth-pgsql libapache2-mod-auth-plain libapache2-mod-php5 libauthen-pam-perl libio-pty-perl libmd5-perl libnet-ssleay-perl libpam-runtime lm-sensors openssl perl php5 php5-cli php5-intl php5-gd php5-imagick php5-curl php5-mcrypt php5-memcache php5-pgsql php5-xcache postgresql postgresql-client postgresql-contrib ssh tetex-base tetex-bin tetex-extra texlive-base-bin zbar-tools

On remote, hosted or dedicated servers the configuration and availability of these applications will depend on the host provider or the operating system that is installed upon the server. If you encounter a problem with your host provider and the use of TCExam check the support and services page.

Configuring DBMS
In order for TCExam to work properly, you will need to have a functioning MySQL or PostgreSQL Database prior to beginning the install process.
TCExam will create a database and the associated tables, provided the details are correctly entered, during the installation process. On occasion however, it may be necessary to create the database ahead of time. Just make a note of the appropriate settings before proceeding with the installation:

The name of your MySQL/PostgreSQL database. This may be pre-set on some hosted server set-ups.
The name of the MySQL/PostgreSQL host. This is usually called "localhost" if you are installing on a PC or a local server. However, if you are using shared hosting, check with your hosting provider to be sure this is the case.
A MySQL/PostgreSQL username. This may have been allocated by your server provider. A local MySQL installation generally has the default administrator username set as "root".
A MySQL/PostgreSQL password. This may have been allocated by your server provider. Local MySQL installation generally has the default administrator password set to a blank field. TCExam always requires a non-blank password. To change the password use the following syntax:
[MySQL]
mysql - u root
UPDATE mysql.user SET Password=PASSWORD('mypassword') WHERE User='root';
FLUSH PRIVILEGES;
quit;
[PostgreSQL]
sudo su postgres -c psql template 1
ALTER USER postgres WITH PASSWORD 'mypassword';
q
Configuring PHP
For the correct use of TCExam, PHP has to be configured to support the systems and libraries indicated above.
Some parameters of PHP must also be set as the following:

php.ini
date.timezone = Europe/Rome ; http://php.net/manual/en/timezones.php
arg_separator.output = “&”
magic_quotes_gpc = On
magic_quotes_runtime = Off
magic_quotes_sybase = Off
request_order = “GPC”
Apache module (/etc/httpd/conf/httpd.conf):
AddDefaultCharset UTF-8
php_value arg_separator.output "&"
php_value magic_quotes_gpc On
php_value magic_quotes_runtime Off
php_value magic_quotes_sybase Off
php_value request_order "GPC"
Installation
When installing TCExam for the first time, verify the system requirements. Assuming you have a working Apache/IIS web server, with PHP and a MySQL/PostgreSQL DBMS, you are on your way to installing TCExam.
If you are getting the TCExam source code for the first time, please rename the "config.default" folders inside admin, public and shared to "config".

TCExam Upgrade
The TCExam upgrade process may vary at each release. Detailed instructions are contained on the UPGRADE.TXT file attached to each TCExam release.

Getting the files
TCExam can be downloaded from GitHub. The file is a compressed archive so you will need an utility program, either locally or on your host server, that can "unzip" the file (i.e. WinZip, WinRAR, 7Zip). Ensure that you choose latest stable release version.

Installing Files
We are assuming you have established a working web server, with the necessary requirements, and that you know where to put files to display on the web server.
Unzip the distribution file into a directory under your web server root. If you are using the Apache web server, this is typically c:apache groupapachehtdocs on the Windows OS and /usr/local/apache/htdocs or /var/www/ on a UNIX-like system but it my vary particularly on hosted servers and between different distributions of GNU-Linux OS.

What you do to install TCExam on a remote host is largely dependant upon the facilities your host provides - with regard to Control Panel software and connection resources. It may also depend upon your own skills concerning server access methods. A simple and typical procedure may involve: unzip the TCExam distribution file to a local directory on your local computer and then FTP the files to the host server placing them either directly under, or in, a directory under the web server root. There are many free FTP programs available for this operation, such as Filezilla. A Google search or visit to any of the open source resource sites will assist you in finding a suitable tool.

When you have finished uploading the files and folders, change the files owner to the Web server user (typically “www-data” or “apache”). On POSIX based systems (like Unix, Linux, etc), change to the TCExam directory and enter the following system command (substitute the user name appropriate for your system): chown -R apache:apache /var/www/tcexam.
Change the files access permission so that all user can write into the them. On POSIX based systems change to the TCExam directory and enter the following system command: chmod -R 777 /var/www/tcexam. For security reasons, you must properly set the permissions of these files at the end of the installation process.

Browser Installation
This type of installation will automatically install the database and will configure the essential system parameters. The installation process will delete any data of previous installations of TCExam, reason why in this case it is advisable to make backup copy of these data.

Point your Web browser (i.e. Mozilla Firefox or Internet Explorer) to the TCExam installation script (http://www.yoursite.com/install/install.php or http://yoursite.com/tcexam_folder/install/install.php). To start the installation you must fill up the form completely and press the button INSTALL.

The required fields are:

db type: type of DBMS (the default is MySQL).
db host: name of the database host (usually localhost).
db port: database port (usually 3306 for MySQL or 5432 for PostgreSQL).
db user: name of the database user (usually it is root for MySQL and postgres for PostgreSQL).
db password: user's password to access the database.
db name: name of the database (usually TCExam). This name has to be changed just when there are other copies of TCExam in the same system.
tables prefix: prefix that will be added to the table names (usually tce_).
host URL: the domain name of your site (i.e. http://www.yoursite.com or https://www.yoursite.com).
relative URL: relative path from the root of your webserver where the TCExam files are located (usually / or /tcexam_folder/).
TCExam path: complete path of the folder where TCExam is installed (i.e. /usr/local/apache/htdocs/TCExam/ or c:/Inetpub/wwwroot/TCExam/).
TCExam port: default connection port (usually 80 for HTTP or 443 for SSL - HTTPS).
If the installation completed succesfully the system is ready for the first execution. At this point you can jump to the Post Installation and Configuration section.
In case the installation did not complete succesfully you can use the manual procedure described in the next section.

Manual Installation
In order to manually install TCExam you must edit some configuration files and install the database.

The essential files and configuration parameters are:

shared/config/cp_db_config.php
K_DATABASE_TYPE (database type, usually MYSQL or POSTGRESQL)
K_DATABASE_HOST (name of the database host, usually localhost)
K_DATABASE_NAME (database name, usually TCExam)
K_DATABASE_USER_NAME (name of the database user, it usually is root)
K_DATABASE_USER_PASSWORD (password to access the database)
K_TABLE_PREFIX (prefix that will be added to the table names, usually tce_)
shared/config/cp_paths.php
K_PATH_HOST (the domain name of your site, i.e. http://www.yoursite.com)
K_PATH_TCEXAM (relative path from the root of your webserver where the TCExam files are located, usually / or /tcexam_folder/)
K_PATH_MAIN (complete path to the folder where TCExam is installed, i.e. /usr/local/apache/htdocs/TCExam/ or c:/Inetpub/wwwroot/TCExam/)
K_STANDARD_PORT (http communication port, usually 80 or 443 for SSL)
Database Installation
In the install folder there are all the SQL files with the structure and data of the database:

mysql_db_structure.sql - Contains the MySQL database structure.
pgsql_db_structure.sql - Contains the PostgreSQL database structure.
db_data.sql - Contains the default database data.
If you want to change the prefix of the tables you must use a text editor with the search and replace function and perform the following substitutions:

In the ..._db_structure.sql file substitute CREATE TABLE tce_ with CREATE TABLE yourprefix
In the db_data.sql file substitute INSERT INTO tce_ with INSERT INTO yourprefix
To execute the SQL files you can use the DBMS commands from the command shell of the server. For MySQL you can use the following syntax:

mysql -u root -p
mysql> CREATE DATABASE TCExam;
mysql> quit
shell> mysql -u root -p TCExam < mysql_db_structure.sql
shell> mysql -u root -p TCExam < db_data.sql
As another option you can use an external DBMS manager (i.e. phpMyAdmin, phpPgAdmin, pgAdmin3, etc.) to create the database and run the SQL files by using the specific commands.

Post Installation and Configuration
Once the installation is completed you must:

delete the install folder since it is not necessary anymore and represent a security issue for the system (rm -fR /var/www/tcexam/install);
there are additional commands required to ensure that files can not be altered unless intended by the administrator; on POSIX system you can use the following commands:
cd /var/www/tcexam
find . -exec chown -R apache:apache {} \;
find . -type f -exec chmod 544 {} \;
find cache/ -type f -exec chmod 644 {} ;
find cache/lang -type f -exec chmod 544 {} \;
find admin/backup -type f -exec chmod 644 {} \;
find admin/log/ -type f -exec chmod 644 {} \;
find public/log/ -type f -exec chmod 644 {} \;
find . -type d -exec chmod 755 {} ;
(n this example /var/www/tcexam is the installation folder, apache is the name of Apache user and group)

configure TCExam to fit your needs and activate additional features.
Configuration
Once the above installation procedure is successfully completed, TCExam will work in "basic" mode. Some additional configuration steps are required in order to activate some features (RADIUS, email, LaTeX) and to personalize some settings to fit your needs. All you have to do is to manually edit the following configuration files:

shared/config/ - Main configuration files:
lang/ - language files
language_tmx.xml - TMX language file (contains all translations)
tce_cas.php - Configuration file for CAS (Central Authentication Service)
tce_config.php - system general configuration
tce_db_config.php - database configuration
tce_email_config.php - general configuration of the email system
tce_general_constants.php - general constants
tce_latex.php - LaTeX configuration
tce_ldap.php - LDAP configuration
tce_mime.php - MIME associations to file extensions
tce_paths.php - file and folder paths within the system
tce_pdf.php - configuration of the format and the headers of the PDF documents
tce_radius.php - RADIUS configuration
tce_user_registration.php - user registration configuration
admin/config/ - Configuration files for the administration area:
tce_auth.php - access levels configuration for the administration modules
tce_config.php - general configuration for the administration panel
public/config/ - Configuration files for the public area:
tce_auth.php - access levels configuration for the public modules
tce_config.php - general configuration for the public area
Configuration files are self-explanatory. If you encounter a problem please check the Support and Services page.

Access and Security
Once the installation and configuration procedures are completed, you can access the administration section by pointing your Web browser to http://www.yoursite.com/tcexam_folder/admin/code/ and using the following username and password:

name: admin
password: 1234
In order to protect your system and be granted with an unique personal access, remember to change the password with the Users form.

To achieve a better level of security you have to protect the whole admin folder with a web-based user autentication system. For Apache check the Apache Authentication, Authorization, and Access Control.
Please protect separately the admin/backupem> folder or move the backup folder to another protected location and set the K_PATH_BACKUP constant in shared/config/tce_paths.php. The content of this directory should not be available via Web browser.
