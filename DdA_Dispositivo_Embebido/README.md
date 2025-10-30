[![ISPC-Logos-2024BFH.jpg](https://i.postimg.cc/7YHBd5Vm/ISPC-Logos-2024BFH.jpg)](https://postimg.cc/LhWBZ6G1)

Repositorio de Sistemas Embebidos - Proyecto IoT Educativo

sistemas-embebidos-iot/
├── 📚 DOCUMENTACION/
│   ├── 📄 Estado_del_arte_IoT_educativo.md
│   ├── 📄 Protocolos_comunicacion_IoT.md
│   ├── 📄 Guia_configuracion_VSCode.md
│   └── 📄 Arquitectura_sistema_completo.md
├── 🔧 HARDWARE/
│   ├── 📄 Endpoint_ESP32C3/
│   │   ├── Esquematico_conexiones.md
│   │   ├── Lista_materiales.md
│   │   └── Pinout_ESP32C3.md
│   ├── 📄 Gateway_ESP32/
│   │   ├── Esquematico_conexiones.md
│   │   ├── Lista_materiales.md
│   │   └── Pinout_ESP32_Acebott.md
│   └── 📄 Sensor_ESP8266/
│       ├── Esquematico_conexiones.md
│       └── Lista_materiales.md
├── 💻 SOFTWARE/
│   ├── 🔹 Endpoint_ESP32C3/
│   │   ├── 📁 src/
│   │   │   ├── main.cpp
│   │   │   ├── comunicacion_rs485.h
│   │   │   ├── comunicacion_lora.h
│   │   │   └── config.h
│   │   ├── platformio.ini
│   │   └── README.md
│   ├── 🔹 Sensor_ESP8266/
│   │   ├── 📁 src/
│   │   │   ├── main.cpp
│   │   │   ├── sensor_aht10.h
│   │   │   ├── comunicacion_rs485.h
│   │   │   └── config.h
│   │   ├── platformio.ini
│   │   └── README.md
│   └── 🔹 Gateway_ESP32/
│       ├── 📁 src/
│       │   ├── main.cpp
│       │   ├── comunicacion_lora.h
│       │   ├── comunicacion_gsm.h
│       │   ├── display_lcd.h
│       │   └── config.h
│       ├── platformio.ini
│       └── README.md
├── ⚙️ CONFIGURACION/
│   ├── c_cpp_properties.json
│   ├── settings.json
│   └── platformio_template.ini
├── 📋 DIAGRAMAS/
│   ├── Arquitectura_sistema.dia
│   ├── Flujo_comunicacion.md
│   └── Secuencia_operacion.md
└── 📄 README.md
# Sistema Embebido IoT para Monitoreo de Sensores

Sistema educativo para monitoreo de temperatura y humedad en silos usando ESP32, ESP8266 y comunicación LoRa/RS485.

## 📋 Descripción del Proyecto
Sistema distribuido para educación en telecomunicaciones que incluye:
- **Sensores ESP8266** con AHT10
- **Endpoint ESP32-C3** como coordinador
- **Gateway ESP32** con GSM y LCD
- Comunicación RS485 + LoRa

## 🛠️ Componentes Hardware
- ESP32-C3 Mini
- ESP32 Acebott
- ESP8266
- Módulos LoRa RA-02
- Módulos MAX485
- Sensores AHT10
- Módulos GSM SimCom 800L

## 📁 Estructura
Consulta cada carpeta para documentación específica y código fuente.
📚 DOCUMENTACION/Estado_del_arte_IoT_educativo.md
markdown
# Estado del Arte en IoT Educativo

## Plataformas Analizadas
- **Grafana**: Visualización limitada en educación
- **MIT App Inventor + IoT**: Accesible pero poca profundidad técnica
- **Broker MQTT**: Comunicación eficiente

## Brecha Identificada
Falta de herramientas visuales, interactivas y abiertas para explorar conceptos de telecomunicaciones IoT.

## Valor Agregado
- Interfaz web simple y moderna
- Enfoque educativo explícito
- Código abierto y documentado
🔧 HARDWARE/Endpoint_ESP32C3/Esquematico_conexiones.md
markdown
# Conexiones EndPoint ESP32-C3 Mini

## Componentes
- 1x ESP32 C3 Mini
- 1x Módulo LoRa RA-02 433MHz
- 1x Módulo MAX485
- 1x Step Down 3.3V
- 1x Step Up 5V
- 1x TP4056 + Batería 18650

## Conexiones LoRa
| ESP32-C3 PIN | LoRa RA-02 | Función |
|-------------|------------|---------|
| GPIO3       | DIO0       | Interrupción |
| GPIO4       | SCK        | SPI Clock |
| GPIO5       | MISO       | SPI MISO |
| GPIO6       | MOSI       | SPI MOSI |
| GPIO7       | CS         | Chip Select |

## Conexiones MAX485
| ESP32-C3 PIN | MAX485 | Función |
|-------------|--------|---------|
| GPIO0       | RO     | Receiver Output |
| GPIO2       | DE+RE  | Control |
| GPIO1       | DI     | Driver Input |
💻 SOFTWARE/Endpoint_ESP32C3/src/main.cpp
cpp
#include <Arduino.h>
#include "comunicacion_rs485.h"
#include "comunicacion_lora.h"
#include "config.h"

#define ENDPOINT_ID "EP01"
#define CICLO_COMPLETO 120000  // 2 minutos

struct SensorData {
    String address;
    String location;
    float temperature;
    float humidity;
};

void ejecutarDiscovery() {
    broadcastRS485("DISCOVERY");
    // Espera respuestas 10 segundos
}

void ejecutarLecturaSensores() {
    // Pide mediciones a cada sensor
}

void enviarDatosLoRa() {
    // Envía datos por LoRa en JSON
}

void setup() {
    Serial.begin(115200);
    inicializarRS485();
    inicializarLoRa();
}

void loop() {
    ejecutarDiscovery();
    delay(10000);
    
    ejecutarLecturaSensores();
    delay(30000);
    
    enviarDatosLoRa();
    delay(15000);
    
    // Espera resto del ciclo
    delay(CICLO_COMPLETO - 55000);
}
⚙️ CONFIGURACION/c_cpp_properties.json
json
{
    "configurations": [
        {
            "name": "Win32",
            "includePath": [
                "${workspaceFolder}/**"
            ],
            "defines": [
                "__DEBUG",
                "UNICODE",
                "_UNICODE"
            ]
        }
    ],
    "version": 4
}
🎯 Características del Repositorio
Documentación completa de hardware y software

Código modular para cada componente del sistema

Configuraciones listas para PlatformIO y VSCode

Diagramas y flujos de comunicación

Guías de solución de problemas comunes

Enfoque educativo con explicaciones detalladas
