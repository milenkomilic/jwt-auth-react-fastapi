# Autenticación JWT con React y FastAPI

Este proyecto implementa un sistema de autenticación basado en JSON Web Tokens (JWT) utilizando React para el frontend y FastAPI para el backend. Incluye una página de inicio de sesión y una página protegida que requiere autenticación.

## Descripción

- **Frontend**: Desarrollado con React, utiliza `react-router-dom` para la navegación y gestiona la autenticación del usuario mediante un formulario de login. Los tokens JWT se almacenan en `localStorage` y se verifican antes de acceder a rutas protegidas.
- **Backend**: Construido con FastAPI, incluye endpoints para generar y verificar tokens JWT, utilizando una base de datos SQLite con SQLAlchemy para almacenar datos (si corresponde).
- **Características**:
  - Formulario de login con validación básica.
  - Ruta protegida que verifica el token JWT.
  - Manejo de errores y estados de carga.

## Requisitos

- **Python 3.11+** (para el backend).
- **Node.js y npm** (para el frontend).
- Git (opcional, para clonar el repositorio).

## Instalación

### 1. Clonar el Repositorio
```bash
  git clone https://github.com/tu-usuario/jwt-auth-react-fastapi.git
  cd jwt-auth-react-fastapi
```

### 2. Configurar el Backend
- Crea un entorno virtual y actívalo:
```bash
  python -m venv venv
  venv\Scripts\activate
```
- Instala las dependencias del backend:
```bash
  pip install -r backend/requirements.txt
```
- Asegúrate de que el archivo backend/database.py tenga la URL de la base de datos configurada (por defecto: sqlite:///./test.db).

### 3. Configurar el Frontend
- Navega al directorio del frontend:
```bash
  cd frontend
```
- Instala las dependencias:
```bash
  npm install
```
- Asegúrate de que react-router-dom esté instalado (si no lo está, instálalo con npm install react-router-dom).

### 4. Ejecutar la Aplicación
- Inicia el backend (desde el directorio backend):
```bash
  uvicorn main:app --reload
```
- Esto ejecutará el servidor en http://localhost:8000.

- Inicia el frontend (desde el directorio frontend):
```bash
  npm start
```
- Esto abrirá la aplicación en http://localhost:3000.

## Uso
- Abre http://localhost:3000 en tu navegador.
- Ingresa un nombre de usuario y contraseña en el formulario de login. (Nota: Debes configurar usuarios válidos en el backend si usas autenticación real).
- Si la autenticación es exitosa, serás redirigido a /protected.
- Si el token no es válido o expira, serás redirigido a la página de login.

## Estructura del Proyecto
```bash
jwt-auth-react-fastapi/
├── backend/               # Código del backend con FastAPI
│   ├── database.py        # Configuración de la base de datos
│   ├── main.py            # Archivo principal de FastAPI
│   ├── models.py          # Definición de modelos de datos
│   ├── requirements.txt   # Dependencias del backend
│   ├── test.db            # Base de datos SQLite (generada al ejecutar)
│   └── venv/              # Entorno virtual (generado al instalar)
├── frontend/              # Código del frontend con React
│   └── auth-app/          # Aplicación React
│       ├── node_modules/  # Dependencias de Node.js
│       ├── public/        # Archivos públicos
│       │   ├── logo.svg   # Logo de la aplicación
│       │   └── ...        # Otros archivos públicos
│       ├── src/           # Código fuente de React
│       │   ├── App.css
│       │   ├── App.js     # Configuración de rutas
│       │   ├── App.test.js
│       │   ├── index.css
│       │   ├── index.js
│       │   ├── login.js   # Componente de login
│       │   ├── protected.js # Página protegida
│       │   ├── reportWebVitals.js
│       │   └── ...        # Otros archivos generados por create-react-app
│       ├── package-lock.json
│       └── package.json
├── README.md              # Este archivo
```
### Configuración Adicional
- Backend: Asegúrate de que el endpoint /token en main.py esté configurado para generar tokens JWT y que /verify-token/{token} verifique los tokens.
- Seguridad: Actualmente, los tokens se almacenan en localStorage, lo cual es vulnerable a ataques XSS. Considera usar cookies HTTP-only en producción.
- Base de Datos: Si necesitas persistencia, configura un esquema de base de datos en database.py y migra los modelos.