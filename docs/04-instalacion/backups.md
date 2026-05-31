# 04 - Copias de seguridad

## 1. Introducción
Este documento describe el sistema de copias de seguridad que se implementará en el servidor LAMP para garantizar la integridad de los datos y permitir la recuperación ante fallos.

## 2. Objetivos de las copias de seguridad
- Proteger la base de datos MariaDB.
- Proteger los archivos de la aplicación web.
- Permitir restauraciones rápidas.
- Automatizar el proceso para evitar errores humanos.

## 3. Elementos a respaldar
- Base de datos: dump completo de MariaDB.
- Aplicación web: contenido de /var/www/html.
- Configuraciones críticas:
  - /etc/apache2
  - /etc/mysql
  - /etc/netdata

## 4. Ubicación de las copias
Las copias se almacenarán en:

/var/backups

Con subcarpetas organizadas por fecha.

## 5. Script de copia de seguridad
Se utilizará un script sencillo ejecutado mediante cron.

Ejemplo de script:

#!/bin/bash

FECHA=$(date +%Y-%m-%d)

mkdir -p /var/backups/$FECHA

# Backup de la base de datos
mysqldump --all-databases > /var/backups/$FECHA/bbdd.sql

> Nota: este volcado incluye las bases de datos, pero en algunos entornos puede ser necesario realizar un backup adicional de la tabla `mysql` si se requiere conservar usuarios y privilegios.


# Backup de la aplicación web
tar -czf /var/backups/$FECHA/www.tar.gz /var/www/html

# Backup de configuraciones
tar -czf /var/backups/$FECHA/configs.tar.gz /etc/apache2 /etc/mysql /etc/netdata

## 6. Programación automática
El script se ejecutará diariamente mediante cron:

0 2 * * * /usr/local/bin/backup.sh

Esto garantiza una copia diaria a las 02:00.

## 7. Restauración básica
Para restaurar:

1. Importar la base de datos:
   mysql < bbdd.sql

2. Restaurar la aplicación web:
   tar -xzf www.tar.gz -C /

3. Restaurar configuraciones:
   tar -xzf configs.tar.gz -C /

> Advertencia: la restauración sobrescribe las bases existentes si ya están creadas, por lo que debe ejecutarse con precaución en entornos de producción.

## 8. Conclusión
El sistema de copias de seguridad propuesto es sencillo, automatizado y suficiente para las necesidades de la PYME, permitiendo una recuperación rápida ante fallos.
