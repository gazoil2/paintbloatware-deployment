# 🎨 Paintbloatware Deployment

Este repositorio contiene la configuración completa para desplegar **Paintbloatware**, incluyendo todos los servicios necesarios: base de datos, almacenamiento, backend (Node/Bun + Prisma), backend en Rust y frontend.

---

## 🚀 Requisitos previos

Antes de comenzar, asegurate de tener instalado:

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

---

## ⚙️ Instalación y despliegue

1. **Clonar el repositorio**

   ```bash
   git clone https://github.com/tuusuario/paintbloatware-deployment.git
   cd paintbloatware-deployment
    ```

2. **Levantar los servicios**
    ```bash
    docker-compose up -d 
    ```
    Esto iniciará:

        🐘 PostgreSQL (Base de datos principal)

        📦 MinIO (Almacenamiento de archivos)

        🧠 Backend Node/Bun (API principal)

        ⚙️ Backend Rust (servicios auxiliares)

        🌐 Frontend (interfaz web)

3. **Ejecutar migraciones de la base de datos**

    Una vez que todos los contenedores estén en marcha, corré las migraciones:
    ```bash
    docker exec -it backend_paintbloatware bun migrate
    ```

4. **Crear un admin**

    Si queres tener acceso crea al menos una cuenta y corre el siguiente comando:
    ```bash
        bun admingenerate
    ```
    

# 🔗 Accesos rápidos

Una vez desplegado, podés acceder a los diferentes servicios desde tu navegador:

| Servicio | URL | Descripción |
|----------|-----|-------------|
| 🌐 **Frontend** | [http://localhost:3000](http://localhost:3000) | Interfaz web principal |
| 🧠 **Backend Node/Bun** | [http://localhost:4000](http://localhost:4000) | API principal |
| ⚙️ **Backend Rust** | [http://localhost:8080](http://localhost:8080) | Servicios auxiliares |
| 📦 **MinIO Console** | [http://localhost:9001](http://localhost:9001) | Panel de administración de almacenamiento |
| 🐘 **PostgreSQL** | `localhost:5432` | Base de datos (acceso directo) |


# 🧰 Comandos útiles

## 🐳 Docker Compose

```bash
# Iniciar todos los servicios
docker-compose up -d

# Detener todos los servicios
docker-compose down

# Ver logs de todos los servicios
docker-compose logs -f

# Ver logs de un servicio específico
docker-compose logs -f backend_paintbloatware

# Reiniciar un servicio
docker-compose restart backend_paintbloatware

# Reconstruir y reiniciar servicios
docker-compose up -d --build

# Eliminar volúmenes (⚠️ elimina datos persistentes)
docker-compose down -v
```

## 🗄️ Base de datos

```bash
# Ejecutar migraciones
docker exec -it backend_paintbloatware bun migrate

# Acceder a la consola de PostgreSQL
docker exec -it postgres_paintbloatware psql -U postgres -d paintbloatware

# Crear backup de la base de datos
docker exec postgres_paintbloatware pg_dump -U postgres paintbloatware > backup.sql

# Restaurar backup
docker exec -i postgres_paintbloatware psql -U postgres paintbloatware < backup.sql
```

### 🔧 Backend

```bash
# Ver logs del backend Node/Bun
docker logs -f backend_paintbloatware

# Reiniciar backend Node/Bun
docker restart backend_paintbloatware

# Ejecutar comandos dentro del contenedor
docker exec -it backend_paintbloatware bun run <comando>

# Ver logs del backend Rust
docker logs -f backend_rust_paintbloatware
```

### 🎨 Frontend

```bash
# Ver logs del frontend
docker logs -f frontend_paintbloatware

# Reiniciar frontend
docker restart frontend_paintbloatware

# Reconstruir solo el frontend
docker-compose up -d --build frontend_paintbloatware
```

### 📦 MinIO

```bash
# Ver logs de MinIO
docker logs -f minio_paintbloatware

# Listar buckets desde CLI
docker exec minio_paintbloatware mc ls local
```

### 🧹 Limpieza

```bash
# Eliminar contenedores detenidos
docker container prune

# Eliminar imágenes sin usar
docker image prune

# Eliminar todo (contenedores, imágenes, volúmenes)
docker system prune -a --volumes
```