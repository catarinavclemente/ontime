---
description: Local configurations
---

# Development environment

### Configure your development environment

The code at the bottom of your _sites/default/settings.php_ file should look like this:

```
// Load environment development override configuration, if available.
// Keep this code block at the end of this file to take full effect.
if (file_exists($app_root . '/' . $site_path . '/settings.override.php')) {
  include $app_root . '/' . $site_path . '/settings.override.php';
}
```

#### Copy example.settings.local.php

Copy _sites/example.settings.local.php_ to sites/default/\_settings.override.php, and [clear the cache](https://drupalize.me/tutorial/clear-drupals-cache).

### How to override configuration

[https://drupalize.me/tutorial/how-override-configuration?p=2458](https://drupalize.me/tutorial/how-override-configuration?p=2458)\
\


Site specs 07-04-2022\
\
After install-clone
-------------------

Administrative theme with a responsive, mobile-first layout and a strong focus on improving the Editorial ExperienceRequires:

* Theme Negotiation by Rules (disabled)\
  dc exec web ./vendor/bin/drush en theme\_rule

Then, enable eJustice Admin Theme.\
dc exec web ./vendor/bin/drush then ejp\_adm\_theme\
\
Then\
dc exec web ./vendor/bin/drush config-set system.theme admin ejp\_adm\_theme

Then\
dc exec web ./vendor/bin/drush cex --no\
\
Analyse... keep calm and carry on

[https://drupalize.me/topic/back-your-drupal-site](https://drupalize.me/topic/back-your-drupal-site)
