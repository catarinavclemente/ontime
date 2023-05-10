---
description: >-
  https://just-ejustice.acc.fpfis.tech.ec.europa.eu/sites/default/files/acc.sql.gz
---

# Database

#### Create a database backup (dump)

You can use Drush to export your database to a _.sql_ text file, like so:\
`drush sql-dump > drupal9.sql`

Where _drupal8.sql_ is whatever meaningful filename you want to use to name your database export.

We're now ready to set up the new instance. The process will be unique to your environment, but you should be able to follow the next steps, at least in general.

{% embed url="https://github.com/ec-europa/toolkit/blob/release/8.x/docs/building-assets.md" %}

Import latest database.\
Go to [https://files.fpfis.tech.ec.europa.eu/index.php/apps/files/?dir=/just-ejustice-reference/mysql\&fileid=149701157](https://files.fpfis.tech.ec.europa.eu/index.php/apps/files/?dir=/just-ejustice-reference/mysql\&fileid=149701157) and download the data base.

Then, run&#x20;

`dcdrush sql:query --file='/home/ec2-user/environment/just-ejustice-reference/[name-of-the-file]gz.sql`
