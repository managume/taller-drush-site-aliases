# Taller Drush Site Aliases

En este taller vamos a ver cómo utilizar los drush site aliases.

## Entornos
Para las siguientes pruebas se utilizarán dos entornos:

* drupal-dev: Este entorno se ejecutará en local utilizando DDEV.
* drupal-live: Este entorno se ha desplegado en un servidor externo.

Para montar Drupal-DEV:
```sh
cd drupal-dev
ddev composer install
# Drush utiliza SSH para ejecutar las diferentes tareas en los entornos remotos, por lo que debemos pasar a DDEV las claves SSH.
ddev auth ssh
```

Para montar Drupal-LIVE:
```sh
cd drupal-live
composer install
# Pre-instalación para que se autogenere el settings.php con un nuevo HASH
drush si --account-name=admin --account-pass=admin
# Importamos el backup
drush sql-cli < backup.sql
drush cr
```
*Nota:* Si tras aplicar el backup hay error en el CSS y el cache-rebuild no lo repara. Acceder a los ajustes de apariencia y dar al botón *Save Configuration*.

## Operaciones habituales

Las siguientes operaciones las ejecutaremos desde el entorno Drupal-DEV, por lo que nos situaremos en el proyecto con `cd drupal-dev`.

### Sincronizar nuestra base de datos con nuestro entorno local
```sh
ddev drush sql-sync @live @self
```
### Limpiar caché de entorno remoto
```sh
ddev drush @live cr
```
### Actualizar base de datos de entorno remoto
```sh
ddev drush @live updb
```
### Listar log de entorno remoto
```sh
ddev drush @live ws
```
### Comprobar actualizaciones de seguridad en entorno remoto
```sh
ddev drush @live ups
```
### Sincronizar carpeta files de mi local con un entorno remoto
```sh
ddev drush rsync @live:%files/ @self:%files
```
*Nota:* En el entorno @live puede que devuelva un error si utilizamos `%files/`, si fuera así bastaría con utilizar la ruta completa a la carpeta `files` acabando siempre con `/`.