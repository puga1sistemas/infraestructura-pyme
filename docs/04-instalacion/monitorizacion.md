# 03 - Monitorización del servidor

## 1. Introducción
Este documento describe la solución de monitorización seleccionada para supervisar el estado del servidor LAMP, incluyendo métricas de rendimiento, uso de recursos y disponibilidad de los servicios principales.

## 2. Objetivos de la monitorización
- Detectar caídas del servicio web.
- Supervisar el uso de CPU, RAM y disco.
- Registrar el estado del servicio Apache.
- Registrar el estado del servicio MariaDB.
- Detectar picos de carga anómalos.
- Facilitar la resolución de incidencias mediante datos históricos.

## 3. Herramienta seleccionada
Se utilizará Netdata, una herramienta ligera y en tiempo real que permite visualizar métricas del sistema desde un panel web accesible únicamente desde la red local.
Además de las métricas principales, pueden incluirse métricas adicionales como la temperatura del sistema y estadísticas de I/O, especialmente útiles en entornos físicos o con alta carga.


### Motivos de la elección
- Instalación sencilla.
- Bajo consumo de recursos.
- Panel web intuitivo.
- Métricas en tiempo real.
- Alertas básicas integradas.

## 4. Instalación prevista
La instalación se realizará mediante el script oficial de Netdata:
### Configuración adicional
Tras la instalación, puede ser necesario ajustar la configuración de Netdata, como limitar el acceso al panel web o activar alertas básicas según las necesidades del sistema.


bash <(curl -Ss https://my-netdata.io/kickstart.sh)

El servicio quedará disponible en:

http://192.168.1.50:19999

Accesible únicamente desde la LAN.

## 5. Servicios monitorizados
- Apache (estado, conexiones activas, tiempo de respuesta)
- MariaDB (consultas por segundo, latencia)
- CPU (carga, procesos)
- RAM (uso total, buffers, caché)
- Disco (lecturas/escrituras, espacio disponible)
- Red (tráfico entrante y saliente)
- Firewall (paquetes permitidos y bloqueados)

## 6. Alertas básicas
Netdata incluye alertas preconfiguradas para:
- Uso elevado de CPU
- Uso elevado de RAM
- Espacio en disco bajo
- Latencia alta en servicios
- Caída del servicio web

Estas alertas se visualizarán en el panel web.

## 7. Conclusión
La solución de monitorización propuesta permite supervisar el estado del servidor de forma sencilla y eficaz, cumpliendo los requisitos del cliente sin añadir complejidad innecesaria.
