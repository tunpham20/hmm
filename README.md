<div align="center">

# HmmmMail

![](https://img.shields.io/badge/version-0.1.1-blue.svg)    ![](https://img.shields.io/badge/php-%3E%3D7.2-green.svg) ![](https://img.shields.io/badge/status-closed--beta-lightgrey.svg)

A **self-hosted** disposable mailbox service (aka trash mail), base on [disposable-mailbox](https://github.com/synox/disposable-mailbox) with little edit :V.

**Demo**: 

[HmmmMail](https://sharelun.com/)
[BhadooMail](https://inbox.bhadoomail.com/inbox/) 

**Screenshot**

![Imgur](https://i.imgur.com/2Lqnp75.png)

</div>
## Features

* Anonymous usage, generate random email addresses. 
* New Mail notification. Download and delete your emails.
* Display emails as text or html with sanitization  filter. 
* Display emails based on one [catch-all imap mailbox](https://www.google.ch/search?q=how+to+setup+catch-all+imap+mailbox).
* Only requires PHP  >=7.2 and [php imap extension](http://php.net/manual/book.imap.php)

## Installation

### Shared Hosting (IMAP Enabled)

Shared Hosting providers like Godaddy and Bluehost provides Full support for IMAP. While several hosts may not provide access to IMAP or SMTP services, in which case contact your hosting provider if they support IMAP extention.

* [Download](https://github.com/HmmmmInc/HmmmMail/releases/latest) the latest release.
* Upload the package into your Hosting Directory where you want to host your mailbox.
* Eg. for example.com/ extract the package into root directory in most cases public_html is the root directory.
* Rename `config.sample.php` to `config.php` and apply the imap settings. Move `config.php` to a safe location in a *parent directory* outside the `public_html`, so it is not reachable through the browser.
* Edit config file using below parameters.

### Configuration (config.php)

The app searches for `config.php` file into the entire directory, to avoid hack move `config.php` file outside the root directory.

* Use IMAP server provided by your Hosting Provider or other provider (such as GMail/GSuite, Yandex, ZohoMail...). For GMail use imap.gmail.com:993/imap/ssl
* Use your username from provider.
* Use your password from provider.

        $config['imap']['url'] = '{ imap.gmail.com:993/imap/ssl}INBOX';
        $config['imap']['username'] = "username";
        $config['imap']['password'] = "password";

* Change email domain with your own domain.

        $config['domains'] = array('example.com', 'example1.com' );

* Add username that can not be accessed.

        $config['blocked_usernames'] = array('root', 'admin', 'temp', 'administrator', 'hostmaster', 'postmaster', 'webmaster');

* Save file. Enjoy

## Other options

### Enable GZIP Compression (For Apache, Litespeed/Openlitespeed only)

* Create/Open `.htaccess` in your `public_html` folder, paste this.

        <ifModule mod_gzip.c>
        mod_gzip_on Yes
        mod_gzip_dechunk Yes
        mod_gzip_item_include file \.(html?|txt|css|js|php|pl)$
        mod_gzip_item_include mime ^application/x-javascript.*
        mod_gzip_item_include mime ^text/.*
        mod_gzip_item_exclude rspheader ^Content-Encoding:.*gzip.*
        mod_gzip_item_exclude mime ^image/.*
        mod_gzip_item_include handler ^cgi-script$
        </ifModule>

* I haven't try with Nginx before, you can try it. [How to?](https://www.google.com/search?q=gzip+nginx&oq=gzip+nginx)

### Enable SSL
* Make sure you have set up SSL certificate forr your website.
* Create/Open `.htaccess` in your `public_html` folder, paste this.

        RewriteEngine On
        RewriteCond %{HTTPS} off
        RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]

* Enjoy :)

### Frontend Design

* Fork the Repo.
* You can edit the file frontend.template.php as per your needs.

## Troubleshooting

* **IMAP Server has invalid certificate**: You might have to add `novalidate-cert` to the IMAP settings. See flags on: http://php.net/manual/en/function.imap-open.php.
* **Error 500, Internal error**: Check your error log file. Add to `config.php`: 

        ini_set('display_errors', 1);   
        ini_set('display_startup_errors', 1);   
        error_reporting(E_ALL);

## Credit

This could not be possible without...

 * https://github.com/synox/disposable-mailbox
 * https://github.com/barbushin/php-imap
 * https://github.com/gnugat-legacy/PronounceableWord
 * http://htmlpurifier.org/