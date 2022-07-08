# Drush

#### Find your site's UUID with Drush

You can find your site's UUID with Drush's `config-get` or `cget` (for short) command. Open Terminal and navigate to the root of your Drupal site. Run the following Drush command:

```php
drush config-get system.site uuid
```

**Tip:** Use the shortcut `drush cget system.site uuid`.

Take note of the long string that is returned. This is your site's UUID.

### Drush commands to administer themes <a href="#page-subtitle" id="page-subtitle"></a>

[https://www.drupal.org/project/drush/issues/530780](https://www.drupal.org/project/drush/issues/530780)
