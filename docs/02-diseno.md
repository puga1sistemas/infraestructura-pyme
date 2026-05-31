# 02 - Diseño de la infraestructura

## 1. Introducción
Este documento describe el diseño técnico de la infraestructura LAMP solicitada por el cliente, incluyendo el diagrama de red lógico y los componentes principales del sistema.

## 2. Arquitectura general
La infraestructura se basa en un único servidor Linux que aloja:
- Servidor web Apache 2.4.x
- Base de datos MariaDB
- Sistema de monitorización
- Servicio SSH para administración
- Firewall UFW

## 3. Componentes del sistema
- **Servidor físico/virtual**: Ubuntu Server 22.04 LTS
- **Red local**: 192.168.1.0/24
- **IP del servidor**: 192.168.1.50
- **Puertos expuestos**:
  - 22 (SSH)
  - 80 (HTTP)
  - 443 (HTTPS)
- **Almacenamiento**:
  - `/var/www/html` para la aplicación web
  - `/var/backups` para copias de seguridad
  - `/var/log` para registros del sistema

## 4. Diagrama de red (lógico)

[Usuarios LAN] ----> [Switch] ----> [Servidor LAMP]
                                   |-- Apache (80/443)
                                   |-- MariaDB
                                   |-- SSH (22)
                                   |-- Monitorización
                                   |-- Firewall UFW

## 5. Flujo de funcionamiento
1. Los usuarios acceden a la aplicación web desde la red local.
2. Apache procesa las peticiones y consulta la base de datos cuando es necesario.
3. El sistema de monitorización registra métricas del servidor.
4. El firewall controla el tráfico entrante.
5. Las copias de seguridad se generan de forma programada.

## 6. Justificación del diseño
- Un único servidor simplifica la administración.
- Apache y MariaDB son tecnologías maduras y ampliamente soportadas.
- La red local proporciona baja latencia.
- La monitorización permite detectar fallos rápidamente.
- La estructura es escalable: se puede añadir un balanceador o separar la base de datos en el futuro.

## 7. Conclusión
El diseño propuesto cumple con los requisitos del cliente y establece una base sólida para el despliegue de la infraestructura. En fases posteriores se documentará la instalación y operación del sistema.
