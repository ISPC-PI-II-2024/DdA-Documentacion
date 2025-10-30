[![ISPC-Logos-2024BFH.jpg](https://i.postimg.cc/7YHBd5Vm/ISPC-Logos-2024BFH.jpg)](https://postimg.cc/LhWBZ6G1)

IoT Monitoring Platform Backend
Una plataforma backend completa para monitoreo IoT construida con Node.js, Express, WebSockets y MQTT.

🚀 Características Principales
Comunicación en Tiempo Real: WebSockets para actualizaciones instantáneas

Integración MQTT: Recepción de datos de sensores IoT en tiempo real

Autenticación Segura: JWT + Google OAuth2

Sistema de Roles: Administrador, Operador y Visualizador

APIs RESTful: Gestión completa de dispositivos y datos

Arquitectura Containerizada: Docker Compose para todos los servicios

Múltiples Bases de Datos: MariaDB (datos estructurados) + InfluxDB (series temporales)

Dashboard y Monitoreo: Integración con Grafana y Node-RED

## 🏗️ Arquitectura del Sistema

### Componentes Principales
┌─────────────────┐ ┌──────────────────┐ ┌─────────────────┐
│ Dispositivos │───▶│ Broker MQTT │───▶│ Backend │
│ IoT │ │ (Mosquitto) │ │ (Node.js) │
└─────────────────┘ └──────────────────┘ └─────────────────┘
│
┌─────────────────┐ │
│ Frontend │◀───────────────────────────────────┤
│ (Cliente) │ │
└─────────────────┘ │
┌──────────────────┐
│ Bases de │
│ Datos │
│ (MariaDB/InfluxDB)│
└──────────────────┘
Servicios Incluidos
Backend Principal: API REST + WebSockets (Express.js)

Base de Datos: MariaDB para datos estructurados

Base de Series Temporales: InfluxDB para métricas

Broker MQTT: Mosquitto para comunicación IoT

Visualización: Grafana para dashboards

Orquestación: Node-RED para flujos de trabajo

Proxy: Nginx Proxy Manager con SSL

Gestión: Portainer para administración de contenedores

📋 Prerrequisitos
Docker y Docker Compose

Node.js 16+ (para desarrollo)

Cuenta de Google Cloud para OAuth2

🛠️ Instalación y Configuración
1. Clonar el Repositorio
bash
git clone https://github.com/tu-usuario/c-prototipo-backend.git
cd c-prototipo-backend
2. Configurar Variables de Entorno
bash
cp .env.example .env
# Editar .env con tus configuraciones
3. Desplegar con Docker Compose
bash
docker-compose up -d
4. Inicializar Base de Datos
bash
# Ejecutar script de inicialización
docker-compose exec mariadb mysql -u root -p < scripts/init-database.sql
🔧 Configuración
Variables de Entorno Clave
env
# Servidor
NODE_ENV=development
PORT=4000

# Autenticación
JWT_SECRET=tu-clave-secreta
GOOGLE_CLIENT_ID=tu-google-client-id

# Base de Datos
MYSQL_HOST=mariadb
MYSQL_DATABASE=silo_db
MYSQL_USER=silo_user
MYSQL_PASSWORD=tu-password

# MQTT
MQTT_BROKER_HOST=mqtt.ispciot.org
MQTT_BROKER_PORT=1883
MQTT_TOPICS=sensors/temperature,sensors/humidity
📡 APIs Disponibles
Autenticación
POST /auth/google - Autenticación con Google OAuth2

POST /auth/dev - Autenticación de desarrollo

Datos de Temperatura
GET /temperature/data - Datos históricos

GET /temperature/stats - Estadísticas

GET /temperature/latest - Última lectura

GET /temperature/mqtt-status - Estado MQTT

Gestión de Dispositivos
GET /devices - Listar dispositivos

GET /devices/:id - Información de dispositivo

GET /devices/:id/sensor-data - Datos del sensor

Configuración
GET /config/general - Configuración general

GET /config/advanced - Configuración avanzada (admin)

PUT /config/advanced - Actualizar configuración (admin)

🔐 Sistema de Seguridad
Roles de Usuario
Administrador: Acceso completo al sistema

Operador: Permisos operacionales limitados

Visualizador: Solo lectura

Autenticación
JWT con expiración configurable

Integración con Google Identity Services

Middleware de verificación de roles

🗃️ Estructura de la Base de Datos
Tablas Principales
usuarios - Gestión de usuarios

dispositivos - Catálogo de dispositivos IoT

datos_sensores - Lecturas de sensores

roles - Sistema de roles y permisos

configuraciones_sistema - Configuraciones

🔄 Flujos de Comunicación
Autenticación
text
Frontend → Google Auth → ID Token → Backend → Verificación → JWT Propio → Frontend
Datos de Temperatura
text
MQTT Broker → mqttService → temperature.controllers → Frontend
WebSockets
text
Cliente → Handshake (JWT) → Conexión WebSocket → Suscripción a tópicos → Datos en tiempo real
🐛 Desarrollo
Ejecutar en Modo Desarrollo
bash
npm install
npm run dev
Scripts Disponibles
bash
npm start          # Producción
npm run dev        # Desarrollo con auto-reload
npm test           # Ejecutar tests
Estructura de Proyecto
text
src/
├── server.js           # Punto de entrada
├── config/             # Configuración
├── controllers/        # Controladores de API
├── middleware/         # Middlewares de seguridad
├── routes/            # Definición de rutas
├── services/          # Lógica de negocio
└── utils/             # Utilidades
📊 Monitoreo y Métricas
Servicios de Visualización
Grafana: http://localhost:3000

Node-RED: http://localhost:1880

Portainer: http://localhost:9000

Endpoints de Salud
GET /health - Estado del servidor

GET /temperature/mqtt-status - Estado conexión MQTT

🚢 Despliegue en Producción
Consideraciones
Configurar SSL/TLS con Nginx Proxy Manager

Establecer políticas de backup automático

Configurar monitoreo y alertas

Implementar rate limiting

Asegurar variables de entorno sensibles

Escalabilidad
Configurar múltiples instancias del backend

Implementar balanceo de carga

Optimizar conexiones a base de datos

Configurar clustering de WebSockets

🤝 Contribución
Fork el proyecto

Crear una rama para tu feature (git checkout -b feature/AmazingFeature)

Commit tus cambios (git commit -m 'Add some AmazingFeature')

Push a la rama (git push origin feature/AmazingFeature)

Abrir un Pull Request

📄 Licencia
Este proyecto está bajo la Licencia MIT - ver el archivo LICENSE para detalles.


