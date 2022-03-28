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

There are two kinds of configuration: simple and complex. Simple configuration is always singular (there is only one instance of itself). A good example for this is the site name and email value items, which are stored inside such a configuration item. There is a singular instance of these value items, because probably there is no need for more. While in the case of a View definition, it follows a certain schema and we can have not a singular one, but multiple View definitions. For this reason, View definition implies a complex configuration.

### What is configuration for?

Configuration is used for storing everything that has to be synchronized between different environments.



Key concepts of the CMI (Configuration Management Initiative):\
\
UUID

When configuration changes are imported, the import files must match the site's UUID.\
Because of this, new environments for a same site, need to be created as clones.

**Sources**\
Sipos, D. (2020). **Drupal 9 Module Development**: Get up and running with building powerful Drupal modules and applications (3rd Edition). Packt Publishing Ltd.\\
