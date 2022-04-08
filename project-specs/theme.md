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

### TWIG debugging

#### Enable Twig debugging options

Enabling Twig debugging involves locating the `twig.config[debug]` settings in your _services.yml_ file and changing their values.

These variables can be edited either directly in _sites/default/services.yml_ or added to the _sites/development.services.yml_ file if you followed the steps above to use a _settings.local.php_ file.

#### Edit the following variables under the `twig.config:` section

```php
debug: true
auto_reload: true
cache: false
```

If you're placing this into your _sites/development.services.yml_ file, add the `twig.config` configuration indented under the `parameters:` line. Ensure that your code additions are appropriately indented with 2 spaces, not the tab character (or an error will result).

```php
parameters:
  twig.config:
    debug: true
    auto_reload: true
    cache: false
```

From a fresh install of Drupal and with the `twig.config` additions, the _sites/development.services.yml_ file now looks like this:

```php
# Local development services.
#
# To activate this feature, follow the instructions at the top of the
# 'example.settings.local.php' file, which sits next to this file.
parameters:
  http.response.debug_cacheability_headers: true
  twig.config:
    debug: true
    auto_reload: true
    cache: false
services:
  cache.backend.null:
    class: Drupal\Core\Cache\NullBackendFactory
```

#### Create a database backup (dump)

You can use Drush to export your database to a _.sql_ text file, like so:\
`drush sql-dump > drupal9.sql`

Where _drupal8.sql_ is whatever meaningful filename you want to use to name your database export.

We're now ready to set up the new instance. The process will be unique to your environment, but you should be able to follow the next steps, at least in general.

[https://github.com/ec-europa/toolkit/blob/release/8.x/docs/building-assets.md](https://github.com/ec-europa/toolkit/blob/release/8.x/docs/building-assets.md)
