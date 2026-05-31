# 01 - Análisis de requisitos del cliente

## 1. Introducción
Este documento recoge los requisitos funcionales y técnicos proporcionados por el cliente para el despliegue de una infraestructura LAMP con capacidades de monitorización, copias de seguridad y operación básica. El objetivo es definir con claridad qué necesita la organización antes de diseñar la arquitectura final.

## 2. Contexto de la empresa
La empresa es una PYME con aproximadamente 15 empleados que requiere una infraestructura estable para alojar una aplicación web interna utilizada para la gestión de proyectos y documentación. Actualmente no dispone de un entorno centralizado ni de procedimientos de operación definidos.

## 3. Requisitos funcionales
- La aplicación web debe estar disponible para todos los empleados desde la red local.
- El sistema debe permitir la autenticación de usuarios.
- La base de datos debe almacenar información de proyectos, tareas y documentos.
- Debe existir un sistema de monitorización que permita detectar fallos o caídas del servicio.
- Se deben generar copias de seguridad automáticas de la base de datos y del contenido web.

### Prioridad de requisitos
Para facilitar la planificación, los requisitos se clasifican en:
- **Críticos:** necesarios para garantizar el funcionamiento básico del sistema.
- **Importantes:** mejoran la operación diaria, pero no bloquean el servicio.
- **Opcionales:** aportan valor añadido y pueden implementarse en fases posteriores.

## 4. Requisitos técnicos
- Servidor web basado en Apache 2.4.x.
- Base de datos MariaDB o MySQL.
- Sistema operativo Linux (Ubuntu Server 22.04 LTS).
- Firewall activo y configurado.
- Acceso remoto mediante SSH.
- Monitorización mediante herramientas ligeras (por ejemplo, Netdata o Prometheus Node Exporter).
- Copias de seguridad programadas mediante scripts o herramientas nativas del sistema.

## 5. Requisitos de seguridad
- Acceso SSH restringido a claves públicas.
- Firewall configurado para permitir únicamente los puertos necesarios (80, 443, 22).
- Actualizaciones de seguridad automáticas.
- Separación de permisos entre servicios.

## 6. Requisitos de disponibilidad
- El servicio web debe estar disponible en horario laboral (08:00–20:00).
- El tiempo máximo de caída aceptable es de 15 minutos.
- Debe existir un procedimiento de recuperación documentado.

## 7. Requisitos de mantenimiento
- El sistema debe ser fácil de actualizar.
- La monitorización debe generar alertas básicas.
- Las copias de seguridad deben poder restaurarse sin intervención compleja.

## 8. Riesgos y limitaciones
- Dependencia de servicios externos para actualizaciones y repositorios.
- Posibles cuellos de botella si la carga de trabajo crece por encima de lo previsto.
- Necesidad de endurecimiento adicional del servidor para minimizar riesgos de seguridad.

## 9. Conclusión
Los requisitos definidos permiten establecer una base clara para el diseño de la infraestructura. A partir de este análisis se elaborará el documento de diseño técnico y el diagrama de red correspondiente.
