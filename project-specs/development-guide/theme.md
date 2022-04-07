# Theme

Drush commands

```ini
theme-enable        => drush theme-enable (drush then)
theme-disable       => drush theme-uninstall (drush thun)
theme-info          => pm-info
theme-list          => pm-list --type=theme
theme-list-enabled  => pm-list --type=theme --status=enabled
theme-set-default   => drush config-set system.theme default [theme_name] 
theme-set-admin     => drush config-set system.theme admin [theme_name] 
theme-status        => status theme
```



<mark style="color:orange;">**Config:**</mark>\ <mark style="color:orange;">**Set default theme in ejp\_profile/config/system.theme.yml**</mark>

#### Create a database backup (dump)

You can use Drush to export your database to a _.sql_ text file, like so:

```php
drush sql-dump > drupal8.sql
```

Where _drupal8.sql_ is whatever meaningful filename you want to use to name your database export.

We're now ready to set up the new instance. The process will be unique to your environment, but you should be able to follow the next steps, at least in general.



[https://github.com/ec-europa/toolkit/blob/release/8.x/docs/building-assets.md](https://github.com/ec-europa/toolkit/blob/release/8.x/docs/building-assets.md)
