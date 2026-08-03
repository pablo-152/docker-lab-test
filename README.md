# Ambiente Docker Test

## Descripción

Este repositorio contiene la configuración del ambiente de desarrollo y pruebas utilizando Docker.

El objetivo es permitir que cualquier desarrollador pueda levantar el mismo ambiente de trabajo sin necesidad de instalar manualmente PHP, Apache o MariaDB en su equipo.

## Tecnologías utilizadas

* Docker Desktop
* Docker Compose
* PHP 7.4
* Apache
* MariaDB 10.3
* phpMyAdmin

---

# Requisitos previos

Antes de iniciar, el desarrollador debe tener instalado:

## Git

Verificar instalación:

```bash
git --version
```

## Docker Desktop

Verificar instalación:

```bash
docker --version
```

```bash
docker compose version
```

## Editor recomendado

Visual Studio Code

Extensiones recomendadas:

* Docker
* PHP Intelephense
* GitLens

---

# Clonar repositorio

Clonar el ambiente:

```bash
git clone https://github.com/pablo-152/docker-lab-test.git
```

Ingresar al proyecto:

```bash
cd docker-lab-test
```

---

# Estructura del proyecto

```text
docker-lab-test
│
├── compose
│   └── docker-compose.yml
│
├── php
│   └── apache-php74
│       └── Dockerfile
│
├── mysql
│   └── README.md
│
├── proyectos
│   └── README.md
│
└── README.md
```

---

# Levantar ambiente Docker

Ingresar a la carpeta donde se encuentra el archivo `docker-compose.yml`:

```bash
cd compose
```

Ejecutar:

```bash
docker compose up -d
```

Verificar contenedores activos:

```bash
docker ps
```

Servicios esperados:

```text
mysql-dev
phpmyadmin-dev
new-snappy-web-test
```

---

# Servicios disponibles

## Aplicación Web

URL:

```
http://localhost:8081
```

---

## phpMyAdmin

URL:

```
http://localhost:8080
```

Configuración:

```
Servidor:
mysql-dev

Usuario:
root

Password:
root123
```

---

## Base de datos MariaDB

Datos de conexión:

```
Host:
localhost

Puerto:
3306

Usuario:
root

Password:
root123
```

Cliente recomendado:

* DBeaver Community

---

# Bases de datos utilizadas

El ambiente utiliza las siguientes bases de datos:

```
snappy_test
ifv_test
kuska_test
laleli_test
```

Los archivos físicos generados por MariaDB no se almacenan en Git.

La restauración de bases de datos debe realizarse mediante backups o scripts SQL proporcionados por el equipo.

---

# Proyectos externos

Los proyectos de desarrollo se manejan en repositorios Git independientes.

Esta carpeta solamente sirve como ubicación donde deben clonarse.

Ejemplo:

```
proyectos
│
├── new_snappy
├── ifv
├── kuska
└── laleli
```

Cada proyecto debe ser clonado dentro de esta carpeta.

Ejemplo:

```bash
cd proyectos

git clone URL_DEL_PROYECTO
```

---

# Detener ambiente

Para detener los contenedores:

```bash
docker compose down
```

---

# Reiniciar ambiente

```bash
docker compose restart
```

---

# Ver logs de contenedores

MariaDB:

```bash
docker logs mysql-dev
```

PHP Apache:

```bash
docker logs new-snappy-web-test
```

phpMyAdmin:

```bash
docker logs phpmyadmin-dev
```

---

# Problemas comunes

## Puerto ocupado

Si algún servicio no inicia, verificar puertos:

```bash
netstat -ano | findstr :3306
```

```bash
netstat -ano | findstr :8080
```

```bash
netstat -ano | findstr :8081
```

---

## Reiniciar completamente el ambiente

```bash
docker compose down

docker compose up -d
```

---

# Recomendaciones para desarrolladores

* No modificar directamente los archivos dentro de `mysql/data`.
* No subir backups grandes de bases de datos al repositorio.
* Mantener actualizado el repositorio antes de iniciar trabajos.
* Cada sistema debe mantener su propio repositorio Git.
* Las configuraciones personales deben manejarse mediante archivos `.env`.

---

# Flujo de trabajo recomendado

Actualizar ambiente:

```bash
git pull
```

Levantar Docker:

```bash
docker compose up -d
```

Ingresar al proyecto correspondiente:

```bash
cd proyectos/nombre_proyecto
```

Realizar desarrollo y subir cambios al repositorio correspondiente.
