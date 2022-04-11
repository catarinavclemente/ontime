# Fresh start - Feeling Good

### Backup

1. ./vendor/bin/drush sql-create -y
2. gunzip < mysql.gz | mysql -uroot -hmysql ejustice
3. ./vendor/bin/run toolkit:run-deploy
4. ./vendor/bin/drush updatedb -y
5. ./vendor/bin/drush cim -y
6. ./vendor/bin/drush cr\
   ``\
   ``
