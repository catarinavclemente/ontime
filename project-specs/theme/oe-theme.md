# OE theme

npm install && npm run build\
./vendor/bin/run toolkit:build-assets\
docker-compose exec web ./vendor/bin/run toolkit:build-assets \
docker-compose exec web ./vendor/bin/drush config-set system.theme default oe\_theme \
docker-compose vendor/bin/run toolkit:build-assets --default-theme=oe\_theme \
docker-compose exec web ./vendor/bin/drush config-set system.theme default oe\_theme \
docker-compose exec web ./vendor/bin/run toolkit:build-assets --default-theme= oe\_theme docker-compose exec web ./vendor/bin/run toolkit:build-assets --validate=check \
docker-compose exec web ./vendor/bin/run toolkit:build-assets --validate
