# Fresh start - Feeling Good

### Install, set-up and clone the project

Run composer install in the web service.\
`docker-compose exec web composer install`\
``\
``Build your development instance of the website.\
`docker-compose exec web ./vendor/bin/run toolkit:build-dev`\
``

VIRTUAL\_HOST=[http://web:8080/web](http://web:8080/web)

``\
``Perform a clone installation with production data.\
`docker-compose exec web ./vendor/bin/run toolkit:install-clone`

### Import configuration using Drush

Check the state of the working directory and the staging area\
Check configurations status:\
`./vendor/bin/drush config:status`

Use the configuration import command alias, `cim` to import configuration.\
`dc exec web ./vendor/bin/drush cim`\
``\
``
