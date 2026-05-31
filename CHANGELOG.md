# CHANGELOG

## Sesión 1 – Análisis inicial del proyecto
### Actividades realizadas
- Definición del alcance del proyecto LAMP para la pyme.
- Identificación de requisitos funcionales y no funcionales.
- Análisis de necesidades de red, seguridad y disponibilidad.
- Redacción del documento `01-analisis.md`.

### Estado general
- Análisis completado.
- Aprobación inicial del cliente.

---

## Sesión 2 – Diseño y planificación
### Actividades realizadas
- Elaboración del diseño de la infraestructura.
- Creación del diagrama de arquitectura.
- Definición de componentes y servicios.
- Redacción del documento `02-diseno.md`.
- Planificación del proyecto y creación del Gantt.
- Redacción del documento `03-planificacion.md`.

### Estado general
- Diseño aprobado.
- Planificación completada.
- Preparación para iniciar la instalación.

---

## Sesión 3 – Intercambio de roles y nuevos documentos
### Documentalista de Plataforma (Jimy)
- Redactado `servidor-web.md` con instalación y configuración de Apache 2.4.60.
- Redactado `base-de-datos.md` con instalación y configuración de MySQL 8.0.
- Actualizado `ssh-firewall.md` con configuración segura de SSH, UFW y Fail2ban.
- Subida la rama `feature/servidor-web-y-bd`.

### Documentalista de Operaciones (David)
- Redactado `05-operacion.md` con tareas de mantenimiento diario.
- Redactado `06-recuperacion.md` con plan de recuperación ante desastres.
- Actualizado `CHANGELOG.md` con los cambios de la sesión.
- Subida la rama `feature/guia-operacion`.

### Estado general
- Roles intercambiados correctamente.
- Nuevos documentos completados.
- Pendiente: abrir PRs y revisión cruzada.

---

## Sesión 4 – Cambio de alcance, HAProxy y pulido final
### Actividades realizadas
- Incorporación del cambio de alcance solicitado por el cliente:
  - Integración de **HAProxy** como balanceador de carga.
  - Actualización de `02-diseno.md` con el nuevo diagrama.
  - Actualización de `03-planificacion.md` con nuevas tareas.
  - Actualización de `servidor-web.md` con la instalación y configuración de HAProxy.
  - Actualización de `05-operacion.md` con tareas de operación del balanceador.

- Revisión cruzada de PRs y merge final en `main`.
- Redacción y subida del README final con enlaces internos.
- Revisión de enlaces internos entre documentos.
- Preparación del repositorio para el release v1.0.

### Estado general
- Cambio de alcance completado.
- Documentación actualizada.
- Repositorio listo para entrega final.
