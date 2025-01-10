# 🌟 Proyecto de Taller 3 - Integración y Despliegue

![GitHub repo](https://img.shields.io/github/repo-size/nico-alvz/taller3?style=flat-square)

Este repositorio contiene los componentes necesarios para el proyecto de Taller 3:

- 📦 **Backend**: Desarrollado en Node.js y desplegado en Render.
- 🎨 **Frontend**: Desarrollado en React y desplegado en Firebase Hosting.

## 📂 Estructura del repositorio

```
├── backend/    # Código fuente del backend
├── frontend/   # Código fuente del frontend
```

## 🌐 URLs del proyecto

- **Frontend**: [https://arq-sistemas-t3.web.app](https://arq-sistemas-t3.web.app/login)
- **Backend**: [https://backend-taller3-pn3v.onrender.com/](https://backend-taller3-pn3v.onrender.com/)

---

## 🚀 Cómo levantar los proyectos

### 📦 Backend

#### 🛠️ Dependencias comunes

1. Tener **Node.js** (v16 o superior) instalado.
2. Tener acceso a una base de datos MySQL configurada.

#### 🔧 Clonar el repositorio

1. Clona el repositorio:

```bash
git clone https://github.com/nico-alvz/taller3.git
cd taller3/backend
```

#### 🔧 Configurar variables de entorno

Crea un archivo `.env` en la carpeta `backend` con las siguientes variables:

```env
DB_HOST=tu_host_mysql
DB_DATABASE=tu_base_datos
DB_USER=tu_usuario
DB_PASSWORD=tu_contraseña
DB_PORT=3306
TOKEN_SECRET=clave_secreta_segura
```

#### 🛠️ Instalar dependencias y correr el servidor localmente

1. Instala las dependencias:

```bash
npm install
```

2. Corre el servidor en modo desarrollo:

```bash
npm run dev
```

El backend estará disponible en `http://localhost:3000`.

#### 🐳 Usar Docker para el Backend

1. Construye la imagen Docker:

```bash
docker build -t backend-taller3:latest .
```

2. Ejecuta el contenedor Docker:

```bash
docker run -d \
  -e DB_HOST=tu_host_mysql \
  -e DB_DATABASE=tu_base_datos \
  -e DB_USER=tu_usuario \
  -e DB_PASSWORD=tu_contraseña \
  -e DB_PORT=3306 \
  -e TOKEN_SECRET=clave_secreta_segura \
  -p 3000:3000 \
  backend-taller3:latest
```

El backend estará disponible en `http://localhost:3000`.

---

### 🎨 Frontend

#### 🔧 Clonar y configurar el repositorio

1. Ve a la carpeta del frontend:

```bash
cd frontend
```

2. Instala las dependencias:

```bash
npm install
```

#### 🛠️ Correr el servidor localmente

1. Para iniciar la aplicación en modo desarrollo:

```bash
npm start
```

La aplicación estará disponible en `http://localhost:3000`.

#### 🚀 Desplegar en producción

1. Compila el proyecto:

```bash
npm run build
```

2. Despliega en Firebase Hosting:

```bash
firebase deploy --only hosting
```

---
