# Servicio de Autenticación

Un microservicio de autenticación ligero construido con FastAPI que proporciona registro de usuarios y autenticación basada en JWT.

## Características
- Registro de usuarios
- Autenticación JWT
- Obtención de información de usuario
- Base de datos SQLite (fácil de configurar, perfecta para implementaciones pequeñas)

## Configuración para Desarrollo Local

### Requisitos Previos
- Python 3.10+
- pip (gestor de paquetes de Python)

### Instalación Local
1. Clonar el repositorio:
```bash
git clone <url-de-tu-repo>
cd <directorio-del-proyecto>
```

2. Crear un entorno virtual:
```bash
python -m venv venv
```

3. Activar el entorno virtual:
```bash
# En Windows:
venv\Scripts\activate

# En Unix o MacOS:
source venv/bin/activate
```

4. Instalar dependencias:
```bash
pip install -r requirements.txt
```

5. Ejecutar la aplicación:
```bash
uvicorn app.main:app --reload
```

La API estará disponible en `http://localhost:8000`

## Despliegue con Docker

### Requisitos Previos
- Docker
- Docker Compose

### Pasos para el Despliegue
1. Construir e iniciar el contenedor:
```bash
docker-compose up --build -d
```

2. Verificar si el contenedor está ejecutándose:
```bash
docker ps
```

La API estará disponible en `http://localhost:8000`

Para detener el servicio:
```bash
docker-compose down
```

## Documentación de la API

Una vez que el servicio esté en ejecución, puedes acceder a:
- Documentación Swagger UI: `http://localhost:8000/docs`
- Documentación ReDoc: `http://localhost:8000/redoc`

### Endpoints Principales

- `POST /register/`: Registrar un nuevo usuario
  ```json
  {
    "email": "usuario@ejemplo.com",
    "username": "nombreusuario",
    "password": "contraseña123"
  }
  ```

- `POST /token`: Iniciar sesión y obtener token de acceso
  - Datos del formulario:
    - username (nombre de usuario)
    - password (contraseña)

- `GET /users/me/`: Obtener información del usuario actual (requiere autenticación)

- `GET /users/`: Obtener lista de todos los usuarios (requiere autenticación)

## Autenticación

Para usar endpoints protegidos:
1. Obtener un token usando el endpoint `/token`
2. Incluir el token en el encabezado de Autorización:
```
Authorization: Bearer <tu-token>
```

## Configuración

La aplicación usa SQLite por defecto. La clave secreta para JWT puede configurarse en el archivo docker-compose.yml:

```yaml
environment:
  - SECRET_KEY=tu-clave-secreta-aqui
```

## Notas de Seguridad

Para despliegue en producción:
1. Cambiar el SECRET_KEY a un valor seguro
2. Asegurar que las reglas de firewall estén correctamente configuradas
3. Considerar usar HTTPS si está expuesto a internet