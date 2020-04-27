# Taller Drush Site Aliases

En este taller vamos a ver cómo utilizar los drush site aliases.

## Levantar entornos
Las pruebas se hacen en local utilizando un entorno Docker gracias a DDEV-Local con configuración NFS activada.

Seguir los siguientes pasos para levantar ambos entornos:

* Drupal-DEV
```sh
cd drupal-dev
ddev start
# En caso de error desactivar la configuración NFS lanzando:
# ddev config --nfs-mount-enabled=false
# ddev start
ddev composer install
ddev drush si -y
```
* Drupal-LIVE
```sh
cd drupal-live
ddev start
# En caso de error desactivar la configuración NFS lanzando:
# ddev config --nfs-mount-enabled=false
# ddev start
ddev composer install
ddev drush sql-cli < backup.sql
```

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
ddev drush @live updb -y
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
