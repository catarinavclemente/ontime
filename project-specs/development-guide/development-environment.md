---
description: Local configurations
---

# Development environment

### Tools for developing in Drupal

Xdebug - PHP debugger\


### Configure your development environment

The code at the bottom of your _sites/default/settings.php_ file should look like this:\


```
// Load environment development override configuration, if available.
// Keep this code block at the end of this file to take full effect.
if (file_exists($app_root . '/' . $site_path . '/settings.override.php')) {
  include $app_root . '/' . $site_path . '/settings.override.php';
}
```

#### Copy example.settings.local.php

Copy _sites/example.settings.local.php_ to _sites/default/_settings.override.php, and [clear the cache](https://drupalize.me/tutorial/clear-drupals-cache).

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

### How to override configuration

[https://drupalize.me/tutorial/how-override-configuration?p=2458](https://drupalize.me/tutorial/how-override-configuration?p=2458)



### Synchronize configuration

The process of configuration sync involves 3 steps:

1. Export: export the full configuration as YAML files from one instance of a site. \
   install-clone
2. Import: stage the configuration on a second instance of the site and compare the differences.\
   `dc exec web ./vendor/bin/drush cim`
3. Synchronize: move the staged configuration from the first site into the active configuration of the second site.\
   \
   Check the state of the working directory and the staging area\
   Check configurations status:\
   `./vendor/bin/drush config:status`\\





Site specs 07-04-2022\
\
After install-clone
-------------------

Administrative theme with a responsive, mobile-first layout and a strong focus on improving the Editorial ExperienceRequires:&#x20;

* Theme Negotiation by Rules (disabled)\
  dc exec web ./vendor/bin/drush en theme\_rule

Then, enable eJustice Admin Theme.\
dc exec web ./vendor/bin/drush then ejp\_adm\_theme\
\
Then \
dc exec web ./vendor/bin/drush config-set system.theme admin ejp\_adm\_theme



Then \
dc exec web ./vendor/bin/drush cex --no\
\
Analyse... keep calm and carry on



[https://drupalize.me/topic/back-your-drupal-site](https://drupalize.me/topic/back-your-drupal-site)
