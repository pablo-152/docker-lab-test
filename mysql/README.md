# Bases de datos

Esta carpeta contiene la documentación relacionada a las bases de datos del ambiente Docker.

Las bases de datos no se almacenan directamente en Git porque contienen archivos físicos del motor MySQL/MariaDB.

Bases utilizadas:

- snappy_test
- ifv_test
- kuska_test
- laleli_test

Para restaurar una base:

1. Iniciar Docker:

docker compose up -d

2. Copiar el backup:

docker cp archivo.sql mysql-dev:/tmp/

3. Restaurar:

docker exec -it mysql-dev mysql -uroot -proot123 nombre_bd < /tmp/archivo.sql