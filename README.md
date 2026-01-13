# docker-pyspark-environment

**Entorno Docker para ejecutar Apache Spark (master/worker) y Jupyter notebooks con PySpark.**

---

## 📋 Tabla de contenidos

- [Descripción](#descripción)
- [Requisitos](#requisitos)
- [Estructura del repositorio](#estructura-del-repositorio)
- [Uso rápido](#uso-rápido)
- [Servicios incluidos](#servicios-incluidos)
- [Notebooks y datos](#notebooks-y-datos)
- [Desarrollo / Personalización](#desarrollo--personalización)

---

## Descripción 💡

Este repositorio contiene una configuración basada en Docker Compose para levantar un clúster básico de Spark (master + worker) y un contenedor con Jupyter que permite ejecutar notebooks con PySpark y acceder a los datos locales montados.

---

## Requisitos 🔧

- Docker (versión reciente)
- Docker Compose (o el plugin integrado `docker compose`)
- Puertos libres en la máquina anfitriona: **8080**, **7077**, **8888**

---

## Estructura del repositorio 📁

- `docker-compose.yml` - definición de los servicios (spark-master, spark-worker, jupyter)
- `jupyter/` - Dockerfile y `requirements.txt` para construir la imagen de Jupyter
- `notebooks/` - notebooks de ejemplo (p. ej. `test.ipynb`)
- `data/` - datasets (p. ej. `vgsales.csv`)

---

## Uso rápido ✅

1. Levantar los servicios:

```bash
docker compose up --build -d
```

2. Abrir Jupyter:

- Accede a: `http://localhost:8888` (el token aparece en los logs del contenedor `spark-jupyter`)
- Para ver logs: `docker compose logs -f jupyter`

3. Interfaz de Spark:

- Spark Master UI: `http://localhost:8080`

4. Detener y limpiar:

```bash
docker compose down
```

---

## Servicios incluidos 🔍

- spark-master
  - Imagen: `apache/spark:4.1.1-...`
  - Puertos: `8080:8080` (UI), `7077:7077` (master)
- spark-worker
  - Se conecta al master vía `spark://spark-master:7077`
- jupyter
  - Construida desde `jupyter/Dockerfile`
  - Monta `./notebooks` y recibe `SPARK_MASTER` en el `environment`

---

## Notebooks y datos 🧪

- Notebook de ejemplo: `notebooks/test.ipynb`
- Dataset incluido: `data/vgsales.csv`

---

## Desarrollo / Personalización 🔧

- Para añadir paquetes a Jupyter, editar `jupyter/requirements.txt` y reconstruir:

```bash
docker compose up --build -d
```

- Si cambias notebooks o datos, están montados en los contenedores para facilitar el desarrollo sin reconstrucción.

---