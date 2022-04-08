# Fresh start - Feeling Good

\


#### Installing the project

```
# Run composer install in the web service.
docker-compose exec web composer install
# Build your development instance of the website.
docker-compose exec web ./vendor/bin/run toolkit:build-dev
# Perform a clean installation of the website.
docker-compose exec web ./vendor/bin/run toolkit:install-clean
# Or alternatively perform a clean installation of the website in
# development mode. This will automatically disable caching and enable
# development modules like devel, devel_generate and kint.
docker-compose exec web ./vendor/bin/run toolkit:install-clean-dev
# Perform a clone installation with production data.
docker-compose exec web ./vendor/bin/run toolkit:install-clone
# Or alternatively perform a clone installation with production data in
# development mode. This will automatically disable caching and enable
# development modules like devel, devel_generate and kint.
docker-compose exec web ./vendor/bin/run toolkit:install-clone-dev
```

\
Synchronize configuration and remove all of the items from GIT index

Check the state of the working directory and the staging area\
Check configurations status:\
`./vendor/bin/drush config:status`

Export: stage the configuration on your dev instance of the site and compare the differences.\
`dc exec web ./vendor/bin/drush cex`\
``\
``This command below will, afterwards, remove all of the items from the Git index (not from the working directory or local repository), and then will update the Git index, while respecting Git ignores. _PS. Index = Cache_

<mark style="background-color:orange;">git rm -r --cached . && git add . && git commit -am "EJPREV: Remove ignored files."</mark>
