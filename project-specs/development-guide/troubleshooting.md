# 🐲 Troubleshooting

PHP Fatal error: Composer detected issues in your platform: Your Composer dependencies require a PHP version ">= 7.4.0". You are running 7.2.24. in /home/ec2-user/environment/just-ejustice-reference/vendor/composer/platform\_check.php on line 24

```php
#sudo amazon-linux-extras disable php7.2 
```

(whichever is the version enabled)

Run

```php
#amazon-linux-extras list | grep php 
```

to list _available_ and _disalbe_ all shows **enabled**

```php
 15  php7.2                          available    \
 17  **lamp-mariadb10.2-php7.2=latest  enabled**      \
  _  php7.3                          available    \
  _  php7.4                          available    [ =stable ]
  _  php8.0                          available    [ =stable ]
```

We might find something like the one highlighted in bold and disable that too eg: `sudo amazon-linux-extras disable lamp-mariadb10.2-php7.2` in the above case.

Once above steps are done try running

```php
sudo amazon-linux-extras enable php7.4
sudo yum install php php7.4-{pear,cgi,common,curl,mbstring,gd,mysqlnd,gettext,bcmath,json,xml,fpm,intl,zip,imap}
```

Once we are done with installation verify

```php
php -v
```

which will give an output similar to the one below
