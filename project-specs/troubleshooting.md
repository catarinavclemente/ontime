# 🐞 Troubleshooting

<mark style="color:red;">**PHP Fatal error: Composer detected issues in your platform: Your Composer dependencies require a PHP version ">= 7.4.0". You are running 7.2.24. in /home/ec2-user/environment/just-ejustice-reference/vendor/composer/platform\_check.php on line 24**</mark>

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

#### <mark style="color:red;">Failed loading /usr/lib64/php/modules/xdebug.so: /usr/lib64/php/modules/xdebug.so: undefined symbol: gc\_globals</mark>

In GNU/Linux systems derived from modern Red Hat releases (such as RHEL, Fedora, and CentOS), the PHP distribution may be divided into the primary .ini file residing at `/etc/php.ini` as well as a collection of other .ini files specific to extensions or packages installed as RPMs residing in `/etc/php.d`. At initialization, PHP will read `/etc/php.d/*.ini` after loading the main `php.ini` file.

It would seem that you have a stale file containing Xdebug settings residing in `/etc/php.d`. Grep for Xdebug in `/etc/php.d` to find the offender and remove it or comment out the relevant lines.

```bash
grep xdebug /etc/php.d/*.ini
```

If Xdebug was installed separately by a manual process and you manually modified the main `/etc/php.ini` to load the extension and configure its settings, that would explain why Xdebug otherwise works while you still see errors about its nonexistence at `/usr/lib/php/modules/xdebug.so`. This also could have happened if configuration files from `/etc` were copied from an old 32bit system to a 64bit system wherein modules reside at `/usr/lib64/php/modules`

\`\`

_<mark style="color:red;">**User warning**</mark>_<mark style="color:red;">**: mkdir(): Permission Denied in**</mark><mark style="color:red;">\*\*</mark> <mark style="color:red;"></mark>_<mark style="color:red;">**Drupal\Component\PhpStorage\FileStorage->createDirectory()**</mark>_ (line\*\*<mark style="color:red;">\*\*</mark> <mark style="color:red;"></mark>_<mark style="color:red;">**123**</mark>_ <mark style="color:red;">**of**</mark> _<mark style="color:red;">**core/lib/Drupal/Component/PhpStorage/FileStorage.php**</mark>_).\*\*

sudo chmod -R 777 web/sites/default/files\
Then, clear the cache.

0/1 \[>-----] 0% Update of openeuropa/oe\_theme failed\ <mark style="color:red;">**Cannot create phar '/home/ec2-user/environment/just-ejustice-reference/vendor/composer/tmp-b8b7a644b84bbce0671024c04f6d**</mark>\ <mark style="color:red;">**01da', file extension (or combination) not recognised or the directory does not exist**</mark>\ <mark style="color:red;">\*\*\*\*</mark>
