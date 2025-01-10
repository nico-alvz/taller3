# Proyecto de Taller 3 - Integración y Despliegue

Este proyecto consta de dos componentes principales:

1. **Backend:** Desarrollado en Node.js y desplegado en Render.
2. **Frontend:** Desarrollado en React y desplegado en Firebase Hosting.

## URLs del proyecto

- **Frontend:** [https://arq-sistemas-t3.web.app/login](https://arq-sistemas-t3.web.app/login)
- **Backend:** [https://backend-taller3-pn3v.onrender.com/](https://backend-taller3-pn3v.onrender.com/)

---

## Levantar el proyecto Backend

### Prerrequisitos

1. Tener **Node.js** (v16 o superior) instalado.
2. Tener acceso a una base de datos MySQL configurada.
3. Instalar **sequelize-cli** globalmente:

```bash
npm install -g sequelize-cli
```

### Variables de entorno
Crea un archivo `.env` en la raíz del proyecto con el siguiente contenido:

```env
DB_HOST=tu-host-mysql
DB_DATABASE=nombre_base_datos
DB_USER=usuario_mysql
DB_PASSWORD=contraseña_mysql
TOKEN_SECRET=una_clave_secreta_segura
```

### Instalación

1. Clona el repositorio:

```bash
git clone <URL_DEL_REPOSITORIO_BACKEND>
cd backend
```

2. Instala las dependencias:

```bash
npm install
```

3. Ejecuta las migraciones y los seeders:

```bash
sequelize db:migrate
sequelize db:seed:all
```

### Ejecutar en desarrollo

Para levantar el servidor en modo desarrollo:

```bash
npm run dev
```

El backend estará disponible en `http://localhost:3000` por defecto.

---

## Levantar el proyecto Frontend

### Prerrequisitos

1. Tener **Node.js** (v16 o superior) instalado.
2. Tener acceso al backend desplegado o en local.

### Instalación

1. Clona el repositorio:

```bash
git clone <URL_DEL_REPOSITORIO_FRONTEND>
cd frontend
```

2. Instala las dependencias:

```bash
npm install
```

### Configuración del entorno
Crea un archivo `.env` en la raíz del proyecto con el siguiente contenido:

```env
REACT_APP_API_URL=https://backend-taller3-pn3v.onrender.com
```

### Ejecutar en desarrollo

Para iniciar la aplicación en modo desarrollo:

```bash
npm start
```

La aplicación estará disponible en `http://localhost:3000`.

### Compilar para producción

Para compilar el proyecto para producción:

```bash
npm run build
```

El contenido compilado se almacenará en la carpeta `build`.

---

## Pipelines de CI/CD con GitHub Actions

### Backend

El pipeline de CI/CD para el backend incluye los siguientes pasos:

1. Construcción de la imagen Docker.
2. Subida de la imagen a Docker Hub.
3. Despliegue del contenedor en Render mediante un webhook.

Archivo de configuración `.github/workflows/backend.yml`:

```yaml
name: Backend CI/CD

on:
  push:
    branches:
      - main

jobs:
  build_and_deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v2

      - name: Log in to Docker Hub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Build and push Docker image
        uses: docker/build-push-action@v3
        with:
          push: true
          tags: ${{ secrets.DOCKER_USERNAME }}/backend-taller3:latest

      - name: Trigger Render deployment
        run: |
          curl -X POST https://api.render.com/deploy/webhooks/<RENDER_WEBHOOK_ID>
```

### Frontend

El pipeline de CI/CD para el frontend incluye:

1. Instalación de dependencias.
2. Construcción del proyecto.
3. Despliegue en Firebase Hosting.

Archivo de configuración `.github/workflows/frontend.yml`:

```yaml
name: Frontend CI/CD

on:
  push:
    branches:
      - main

jobs:
  build_and_deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 16

      - name: Install dependencies
        run: npm install

      - name: Build project
        run: npm run build

      - name: Deploy to Firebase Hosting
        run: firebase deploy --only hosting
        env:
          FIREBASE_TOKEN: ${{ secrets.FIREBASE_TOKEN }}
```

---

