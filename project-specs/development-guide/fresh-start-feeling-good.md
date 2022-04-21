# Fresh start - Feeling Good

&#x20;**./vendor/bin/run toolkit:download-dump --dumpfile dump.sql**

### Backup

1.

    ```
    drush cr
    drush sql-dump > ~/new.sql
    ```
2. Creating database ejustice. Any existing database will be dropped!\
   `./vendor/bin/drush sql-create -y`&#x20;
3. docker-compose exec web ./vendor/bin/drush sql-dump > ejustice.sql
4. gunzip < mysql.gz | mysql -uroot -hmysql ejustice
5. ./vendor/bin/run toolkit:run-deploy
6. ./vendor/bin/drush updatedb -y
7. ./vendor/bin/drush cim -y
8. ./vendor/bin/drush cr\
   ``\
   ``
