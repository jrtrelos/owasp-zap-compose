# OWASP ZAP + Juice Shop Security Lab

Este proyecto proporciona un entorno de laboratorio listo para usar para pruebas de seguridad de aplicaciones dinámicas (DAST), utilizando **OWASP ZAP** (Zed Attack Proxy) como escáner y **OWASP Juice Shop** como aplicación objetivo vulnerable.

## 🚀 Descripción del Entorno

El laboratorio consta de dos servicios principales orquestados con Docker Compose:

1.  **OWASP Juice Shop**: Probablemente la aplicación web más moderna y sofisticada con fines de entrenamiento en seguridad. Incluye vulnerabilidades de todo el OWASP Top 10.
2.  **OWASP ZAP**: La herramienta de seguridad web gratuita y de código abierto más utilizada en el mundo. Configurada aquí con una interfaz web (Webswing) para facilitar su uso desde cualquier navegador.

## 📋 Requisitos Previos

Asegúrate de tener instalados los siguientes componentes en tu sistema:

*   **Docker**: Versión 20.10 o superior.
*   **Docker Compose**: Plugin de Docker o versión independiente V2.

## 🛠️ Instalación y Ejecución

Sigue estos pasos para poner en marcha tu laboratorio:

1.  **Clonar el repositorio** (si aún no lo has hecho):
    ```bash
    git clone https://github.com/jrtrelos/owasp-zap-compose.git
    cd owasp-zap-compose
    ```

2.  **Iniciar los servicios**:
    ```bash
    docker compose up -d
    ```

3.  **Verificar que los contenedores estén corriendo**:
    ```bash
    docker compose ps
    ```

## 🌐 URLs de Acceso

Una vez que los servicios estén en marcha, puedes acceder a ellos a través de las siguientes URLs:

| Servicio | URL | Descripción |
| :--- | :--- | :--- |
| **OWASP Juice Shop** | [http://localhost:3000](http://localhost:3000) | Aplicación objetivo vulnerable. |
| **OWASP ZAP (Web UI)** | [http://localhost:8080](http://localhost:8080) | Interfaz de usuario de ZAP vía Webswing. |
| **OWASP ZAP (Proxy/API)** | `http://localhost:8090` | Puerto configurado para el Proxy y la API. |

## 📂 Estructura del Proyecto

```text
.
├── docker-compose.yml    # Orquestación de servicios
├── README.md             # Documentación del proyecto
└── zap/
    └── reports/          # Directorio persistente para reportes de ZAP
        └── .gitkeep      # Asegura que el directorio exista en Git
```

## 🏗️ Arquitectura Docker

La arquitectura implementada se basa en los siguientes principios:

*   **Aislamiento de Red**: Ambos servicios operan dentro de una red privada virtual de Docker denominada `zap-net`. Esto permite que ZAP se comunique con Juice Shop utilizando el nombre del servicio (`http://juice-shop:3000`) de forma interna.
*   **Persistencia de Datos**: Se utiliza un volumen montado de host (`./zap/reports`) para asegurar que cualquier reporte de seguridad generado por ZAP se guarde localmente y persista tras reiniciar los contenedores.
*   **Gestión de Ciclo de Vida**: Se utiliza la política `restart: unless-stopped` para garantizar que los servicios estén disponibles automáticamente después de un reinicio del sistema, a menos que se detengan explícitamente.
*   **Arquitectura Moderna**: Se omite la propiedad `version` en el archivo Compose para cumplir con las especificaciones más recientes y evitar mensajes de advertencia.

---
*Desarrollado para propósitos educativos y de pruebas de seguridad.*
