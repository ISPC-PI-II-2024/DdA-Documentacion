Web App - IoT Monitoring Platform
Una aplicación web moderna para monitoreo en tiempo real de dispositivos IoT, construida con JavaScript vanilla y arquitectura reactiva.

🚀 Características Principales
Interfaz Reactiva: Estado global con patrón Pub/Sub

Tiempo Real: WebSockets con autenticación JWT

Autenticación Segura: Google OAuth 2.0 integrado

Control de Acceso: Sistema de roles (Admin, Action, Readonly, Guest)

Visualización Avanzada: Gráficos canvas optimizados y SVG interactivo

Diseño Responsive: Compatible con múltiples dispositivos

SPA: Single Page Application con enrutamiento basado en hash

🏗️ Arquitectura Técnica
Stack Tecnológico
Frontend: JavaScript ES6+ vanilla

Estado: Store reactivo con Pub/Sub

Comunicación: WebSockets + REST APIs

Autenticación: Google Identity Services

Estilos: CSS3 con diseño modular

Build: Módulos ES6 nativos

Estructura de Proyecto
text
src/
├── app.js                 # Punto de entrada principal
├── api.js                 # Cliente HTTP y gestión de sesión
├── config.js             # Cargador de configuración
├── router/               # Sistema de enrutamiento SPA
├── state/                # Gestión de estado global
├── components/           # Componentes reutilizables
├── pages/                # Vistas de la aplicación
├── services/             # Servicios de datos
├── utils/                # Utilidades y helpers
└── assets/               # Recursos estáticos
📦 Componentes Principales
Estado Global (Store)
javascript
const state = {
    user: null,           // Usuario autenticado
    role: 'guest',        // Rol actual
    currentProject: null, // Proyecto activo
    selectedDevice: null, // Dispositivo seleccionado
    devices: []          // Lista de dispositivos
};
Sistema de Rutas
"/" - Login (pública)

"/dashboard" - Panel principal

"/dispositivos" - Gestión de dispositivos

"/configuracion" - Configuración general

"/configuracion/avanzada" - Admin only

"/sobre-nosotros" - Información del proyecto

Servicios Especializados
DeviceService: Gestión de dispositivos IoT con cache

MQTTTopicsService: Administración de tópicos MQTT

ConfigService: Configuración persistente

CacheService: Cache en memoria con TTL

RTCClient: Cliente WebSocket en tiempo real

🎨 Interfaces de Usuario
Dashboard Principal
Vista general del estado del sistema

Widgets de métricas en tiempo real

Selector de dispositivos con búsqueda

Visualización SVG interactiva de dispositivos

Gráficos de datos con actualización automática

Gestión de Dispositivos
Listado con análisis de estado crítico

Detección automática de anomalías

Indicadores visuales de estado (LEDs)

Filtrado y búsqueda en tiempo real

Paneles de Configuración
General: Preferencias de usuario

Avanzada: Administración del sistema (solo admin)

Umbrales de temperatura y alertas

Configuración MQTT y notificaciones

🔧 Instalación y Desarrollo
Prerrequisitos
Servidor web estático (nginx, Apache, o servidor de desarrollo)

Backend IoT configurado y ejecutándose

Google OAuth Client ID configurado

Configuración Inicial
Clonar el repositorio

Configurar config.json con los endpoints del backend

Establecer variables de entorno necesarias

Estructura de Configuración
json
{
  "API_URL": "http://localhost:4000/api",
  "WS_URL": "ws://localhost:4000/ws", 
  "GOOGLE_CLIENT_ID": "tu-client-id"
}
Desarrollo Local
bash
# Usar servidor de desarrollo local
npx serve src/

# O con Python
python -m http.server 8080 --directory src/
🔌 Integración con Backend
Endpoints Consumidos
GET /api/config/general - Configuración pública

POST /api/auth/google - Autenticación OAuth

GET /api/devices - Lista de dispositivos

GET /api/temperature/* - Datos de sensores

GET /api/config/advanced - Configuración admin

WebSocket Events
sub - Suscribirse a tópicos

unsub - Cancelar suscripción

Mensajes en formato: {topic, ts, payload}

👥 Sistema de Roles
Jerarquía de Permisos
Guest: Acceso limitado, solo vistas públicas

Readonly: Lectura de datos y monitoreo

Action: Lectura + acciones operacionales básicas

Admin: Acceso completo + configuración del sistema

Protección de Rutas
javascript
const routes = {
  "configuracion/avanzada": {
    view: () => import("../pages/configuracionAvanzada.js"),
    meta: { roles: ["admin"] }  // Solo administradores
  }
};
🎯 Características Avanzadas
Visualización en Tiempo Real
Gráficos canvas optimizados a 60 FPS

Buffer circular para datos históricos

Escalado automático de ejes

Suscripción automática a tópicos MQTT

Gestión de Estado
Store reactivo con notificaciones de cambios

Persistencia de sesión en sessionStorage

Cache inteligente con invalidación automática

Sistema de eventos personalizados

Experiencia de Usuario
Loading states y skeletons

Manejo elegante de errores

Notificaciones del navegador

Diseño responsive y accesible

🚢 Despliegue
Build para Producción
bash
# La aplicación usa módulos ES6 nativos
# No requiere build step, pero se puede optimizar con:
npm install -g rollup
rollup -c  # Si se configura rollup.config.js
Servidor Web
Configurar servidor web para servir src/ como raíz y manejar rutas SPA:

Ejemplo nginx:

nginx
location / {
    try_files $uri $uri/ /index.html;
}
Variables de Entorno
bash
# En producción, configurar:
API_URL=https://tu-backend.com/api
WS_URL=wss://tu-backend.com/ws
GOOGLE_CLIENT_ID=tu-client-id-de-produccion
🤝 Contribución
Estructura de Código
Módulos ES6 con import/export

Funciones puras cuando sea posible

Eventos personalizados para comunicación entre componentes

CSS modular con prefijos de componentes

Convenciones
Components: camelCase para funciones

Pages: render como función principal

Services: Clases con métodos estáticos cuando sea posible

Utils: Funciones puras y helpers

📄 Licencia
Este proyecto es parte del programa educativo ISPC - Tecnicatura Superior en Telecomunicaciones, Cohorte 2024.

🆘 Soporte
Para issues y consultas técnicas:

Revisar documentación técnica en /docs

Verificar configuración de endpoints

Validar tokens de Google OAuth

Revisar consola del navegador para errores

