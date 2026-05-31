# 02 - Diseño de la infraestructura

## 1. Introducción
Este documento describe el diseño técnico de la infraestructura necesaria para desplegar una aplicación web basada en una pila LAMP, incluyendo los componentes de red, seguridad, monitorización y copias de seguridad.

## 2. Arquitectura general
La infraestructura se basa en un único servidor Linux que alojará los siguientes componentes:

- Balanceador de carga HAProxy situado delante del servidor web para gestionar el tráfico entrante y permitir futuras ampliaciones del servicio.
- Servidor web Apache 2.4.x
- Base de datos MariaDB/MySQL
- Servicio SSH para administración remota
- Sistema de monitorización ligero
- Scripts o herramientas para copias de seguridad

### Tabla de versiones de software

| Software | Versión | Descripción |
|----------|---------|-------------|
| HAProxy  | 2.x     | Balanceador de carga frontal |
| Apache   | 2.4.60  | Servidor web |
| MySQL    | 8.0     | Base de datos |
| Certbot  | 2.9     | SSL/TLS automático |


### Diagrama lógico
Se incluirá un **diagrama lógico** que represente la relación entre los componentes principales: servidor web, base de datos, firewall, red interna y servicios auxiliares. Este diagrama se añadirá en la fase final de diseño.

### Integración del balanceador HAProxy

El diseño se amplía para incluir un **balanceador de carga HAProxy** situado delante del servidor web Apache. La relación entre componentes queda así:

- Clientes (HTTP/HTTPS)
  → **Balanceador HAProxy**
  → Servidor web Apache
  → Base de datos MySQL/MariaDB
  → Servicios auxiliares (monitorización y copias de seguridad)

El balanceador actúa como punto de entrada único y permite escalar horizontalmente el servicio web en el futuro.


## 3. Diseño de red
- El servidor estará conectado a la red interna de la empresa.
- Se utilizará una IP estática.
- El firewall permitirá únicamente los puertos necesarios:
  - 80 (HTTP)
  - 443 (HTTPS)
  - 22 (SSH)

## 4. Diseño de seguridad
- Acceso SSH restringido a claves públicas.
- Firewall configurado con reglas mínimas necesarias.
- Actualizaciones de seguridad automáticas activadas.

### Endurecimiento básico del servidor
Además de las medidas anteriores, se considerarán acciones de **endurecimiento básico**, como:
- Deshabilitar el acceso SSH del usuario root.
- Configurar herramientas como *fail2ban* para mitigar intentos de acceso no autorizado.

## 5. Diseño de monitorización
- Instalación de una herramienta ligera como Netdata o Node Exporter.
- Configuración de alertas básicas.
- Visualización del estado del sistema en tiempo real.

## 6. Diseño de copias de seguridad
- Copias automáticas de la base de datos mediante `mysqldump`.
- Copias del contenido web mediante `tar` o herramientas equivalentes.
- Almacenamiento local y posibilidad de exportación externa.

## 7. Conclusión
El diseño propuesto establece una infraestructura sencilla, segura y adecuada para las necesidades de la empresa. El siguiente paso será la implementación y validación del entorno.
