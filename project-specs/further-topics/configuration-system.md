---
description: >-
  First, we'll define configuration in Drupal's context, what it is used for and
  what options we have for managing it in Drupal, both as a site builder and as
  a developer.
---

# Configuration system

### What is configuration?

\
Configuration, in Drupal, is the data that the proper functioning of an application relies upon.

In versions prior to Drupal 8, data was simply stored in the database and the lack of consistency of Features or Ctools exportables meant big risks and headaches for Drupal developers.

Since Drupal 8, the configuration system (CS) is, therefore, an indispensable tool.

There are two types of configuration: simple and configuration entities. In this [article](https://www.drupal.org/node/2120523#s-simple-configuration-vs-configuration-entities), you can have a more deep analysis of this.\
\
Configuration entities is a type of configuration which you would empower a user to create and configure one or more times, in order to be used in some other configuration form, like image styles or views.

### What is configuration for?

Configuration is used for storing everything that has to be synchronized between different environments.

The typical flow is for the active site configuration to be synchronized with the one in the YAML files. This means importing all the configurations which are new or different in the YAML files into the database. These YAML files are inside the configuration sync folder, which should be committed to Git (you can configure in the `settings.php`, which directory should be the`sync` folder) and the opposite is to export the active configuration to the YAML files in order to commit them into code.

The UI allows you to compare the configuration uploaded to your sync directory with the active one on the database by providing you with a nice Diff interface.\
\
Then, you synchronize either in the UI as we've seen, or through Drush.\
\
You should check the configuration status regularly with the commands, bellow:\
`docker-compose exec web ./vendor/bin/drush config:status`

To export to sync directory, your changes into the DB:\
`docker-compose exec web ./vendor/bin/drush cex`

To import configuration from sync directory, overriding your changes in the DB: Execute: docker-`docker-compose exec web ./vendor/bin/drush cim`

### Configuration storage

Configuration can be stored either in YAML files (the sync storage) or in the database (the active storage).

If a configuration is mandatory for our code to work, we can create it upon module installation.\
There are two ways this can be done:\
**Statically (most common way):** including YAML files in a config/install folder of the module, so that they get imported when the module is installed.\
**Dynamically (if the values we need to set in the configuration must be retrieved dynamically):** implementing a hook\_install(), so that we can try to get our value and create the configuration object containing it.

However, with optional configuration, you can provide configuration files with the module that should only be imported if their dependencies are met. Meaning that if the dependencies of these configurations are not met (modules, themes and other configurations), the module will install correctly but without those configurations.

****

### Schema

Schema allows various systems to interact properly with the configuration items. They are a way to define the configuration items and specify what kind of data they store (strings, Booleans, integers and so on).\
The **schema** or structure for the image style configuration entity is defined in _core/modules/image/config/schema/image.schema.yml_.

Key concepts of the CMI (Configuration Management Initiative):\
\
UUID

When configuration changes are imported, the import files must match the site's UUID.\
Because of this, new environments for a same site, need to be created as clones.

**Sources**\
Sipos, D. (2020). **Drupal 9 Module Development**: Get up and running with building powerful Drupal modules and applications (3rd Edition). Packt Publishing Ltd.\\

[https://drupalize.me/tutorial/what-are-configuration-entitie](https://drupalize.me/tutorial/what-are-configuration-entitie)

[https://www.drupal.org/node/2120523#s-simple-configuration-vs-configuration-entities](https://www.drupal.org/node/2120523#s-simple-configuration-vs-configuration-entities)
