# HmmmMail

![](https://img.shields.io/badge/version-0.1b-blue.svg)    ![](https://img.shields.io/badge/php-%3E%3D7.2-green.svg) ![](https://img.shields.io/badge/status-beta-lightgrey.svg)

A **self-hosted** disposable mailbox service (aka trash mail) base on [disposable-mailbox](https://github.com/synox/disposable-mailbox) with little edit :V.

**Demo**: 
* [HmmmMail](https://sharelun.com/)
* [BhadooMail](https://inbox.bhadoomail.com/inbox/) 

**Screenshot**

![Imgur](https://i.imgur.com/2Lqnp75.png)

## Features

* Anonymous usage, generate random email addresses. 
* New Mail notification. Download and delete your emails.
* Display emails as text or html with sanitization  filter. 
* Display emails based on one [catch-all imap mailbox](https://www.google.ch/search?q=how+to+setup+catch-all+imap+mailbox).
* Only requires PHP  >=7.2 and [php imap extension](http://php.net/manual/book.imap.php)

### Installation

### Shared Hosting (IMAP Enabled)

Shared Hosting providers like Godaddy and Bluehost provides Full support for IMAP. While several hosts may not provide access to IMAP or SMTP services, in which case contact your hosting provider if they support IMAP extention.

* [Download](https://github.com/HmmmmInc/HmmmMail/releases/latest) the latest release.
* Upload the package into your Hosting Directory where you want to host your mailbox.
* Eg. for example.com/ extract the package into root directory in most cases public_html is the root directory.
* Rename `config.sample.php` to `config.php` and apply the imap settings. Move `config.php` to a safe location in a *parent directory* outside the `public_html`, so it is not reachable through the browser.
* Edit config file using below parameters.

## Configuration (config.php)

The app searches for config.php file into the entire directory, to avoid hack move the file outside the root directory.

* Use IMAP server provided by your Hosting Provider. For GMail use imap.gmail.com:993/imap/ssl
* Use your username from Provider.
* Use your password from Provider.

        $config['imap']['url'] = '{ imap.gmail.com:993/imap/ssl}INBOX';
        $config['imap']['username'] = "username";
        $config['imap']['password'] = "password";

* Change emails domain with your own domain.

        $config['domains'] = array('example.com', 'example1.com' );

* Add username that can not be accessed.

        $config['blocked_usernames'] = array('root', 'admin', 'temp', 'administrator', 'hostmaster', 'postmaster', 'webmaster');
* Save file. Enjoy

## Enable GZIP Compression (For Apache, Litespeed/Openlitespeed only)
* Create/Open .htaccess in your `public_html` folder, paste this.

        <IfModule mod_deflate.c>
        # Compress HTML, CSS, JavaScript, Text, XML and fonts
        AddOutputFilterByType DEFLATE application/javascript
        AddOutputFilterByType DEFLATE application/rss+xml
        AddOutputFilterByType DEFLATE application/vnd.ms-fontobject
        AddOutputFilterByType DEFLATE application/x-font
        AddOutputFilterByType DEFLATE application/x-font-opentype
        AddOutputFilterByType DEFLATE application/x-font-otf
        AddOutputFilterByType DEFLATE application/x-font-truetype
        AddOutputFilterByType DEFLATE application/x-font-ttf
        AddOutputFilterByType DEFLATE application/x-javascript
        AddOutputFilterByType DEFLATE application/xhtml+xml
        AddOutputFilterByType DEFLATE application/xml
        AddOutputFilterByType DEFLATE font/opentype
        AddOutputFilterByType DEFLATE font/otf
        AddOutputFilterByType DEFLATE font/ttf
        AddOutputFilterByType DEFLATE image/svg+xml
        AddOutputFilterByType DEFLATE image/x-icon
        AddOutputFilterByType DEFLATE text/css
        AddOutputFilterByType DEFLATE text/html
        AddOutputFilterByType DEFLATE text/javascript
        AddOutputFilterByType DEFLATE text/plain
        AddOutputFilterByType DEFLATE text/xml
        # Remove browser bugs (only needed for really old browsers)
        BrowserMatch ^Mozilla/4 gzip-only-text/html
        BrowserMatch ^Mozilla/4\.0[678] no-gzip
        BrowserMatch \bMSIE !no-gzip !gzip-only-text/html
        Header append Vary User-Agent
        </IfModule>
* I haven't try with Nginx before, you can try ít. [How to?](https://www.google.com/search?q=gzip+nginx&oq=gzip+nginx)

## Enable SSL
* Make sure you have set up SSL certificate forr your website.
* Create/Open .htaccess in your `public_html` folder, paste this.

        RewriteEngine On
        RewriteCond %{HTTPS} off
        RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]

* Ejnoy :)

## Frontend Design

* Fork the Repo.
* You can edit the file frontend.template.php as per your needs.

### Troubleshooting

* **IMAP Server has invalid certificate**: You might have to add `novalidate-cert` to the IMAP settings. See flags on: http://php.net/manual/en/function.imap-open.php.
* **Error 500, Internal error**: Check your error log file. Add to `config.php`: 

        ini_set('display_errors', 1);    ini_set('display_startup_errors', 1);    error_reporting(E_ALL);

## Credit
This could not be possible without...
 * https://github.com/barbushin/php-imap
 * https://github.com/gnugat-legacy/PronounceableWord
 * http://htmlpurifier.org/, 
 * https://github.com/synox/disposable-mailbox