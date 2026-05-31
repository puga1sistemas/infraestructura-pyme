# Documentación del despliegue de infraestructura LAMP con monitorización

## Autores
- **David** — Documentalista de plataforma  
- **Jimy** — Documentalista de operaciones

## Descripción del proyecto
Este repositorio contiene la documentación completa del despliegue de una infraestructura LAMP para una pyme, abarcando análisis, diseño, planificación, instalación, operación y recuperación ante desastres.

Durante la Sesión 4 se incorporó un cambio de alcance solicitado por el cliente: la integración de un balanceador de carga **HAProxy** delante del servidor Apache.  
Los documentos afectados han sido actualizados para reflejar este cambio.

---

# Estructura del repositorio

```
.
├── CHANGELOG.md
├── docs
│   ├── 01-analisis.md
│   ├── 02-diseno.md
│   ├── 03-planificacion.md
│   ├── 04-instalacion
│   │   ├── backups.md
│   │   ├── base-de-datos.md
│   │   ├── monitorizacion.md
│   │   ├── servidor-web.md
│   │   └── ssh-firewall.md
│   ├── 05-operacion.md
│   └── 06-recuperacion.md
├── README.md
└── tareas.md
```

---

# Documentación

A continuación se presentan los documentos principales del proyecto, con enlaces internos y una breve descripción de cada uno.

## 1. Análisis  
**Documento:** [docs/01-analisis.md](docs/01-analisis.md)  
Incluye el análisis inicial de requisitos, alcance, necesidades de la pyme y justificación técnica de la solución LAMP.

## 2. Diseño  
**Documento:** [docs/02-diseno.md](docs/02-diseno.md)  
Contiene el diseño de la infraestructura, el diagrama de arquitectura y la tabla de componentes.  
Incluye la actualización correspondiente al cambio de alcance con HAProxy.

## 3. Planificación  
**Documento:** [docs/03-planificacion.md](docs/03-planificacion.md)  
Incluye el cronograma del proyecto, el Gantt y la planificación de tareas.  
Actualizado para reflejar las tareas adicionales del balanceador HAProxy.

## 4. Instalación  
Carpeta: [docs/04-instalacion](docs/04-instalacion)

- **Servidor web (Apache + HAProxy):**  
  [docs/04-instalacion/servidor-web.md](docs/04-instalacion/servidor-web.md)

- **Base de datos (MariaDB/MySQL):**  
  [docs/04-instalacion/base-de-datos.md](docs/04-instalacion/base-de-datos.md)

- **SSH y firewall:**  
  [docs/04-instalacion/ssh-firewall.md](docs/04-instalacion/ssh-firewall.md)

- **Monitorización:**  
  [docs/04-instalacion/monitorizacion.md](docs/04-instalacion/monitorizacion.md)

- **Backups:**  
  [docs/04-instalacion/backups.md](docs/04-instalacion/backups.md)

## 5. Operación  
**Documento:** [docs/05-operacion.md](docs/05-operacion.md)  
Incluye las tareas de operación, mantenimiento y supervisión de la infraestructura.  
Actualizado con las tareas de operación del balanceador HAProxy.

## 6. Recuperación  
**Documento:** [docs/06-recuperacion.md](docs/06-recuperacion.md)  
Describe los procedimientos de recuperación ante fallos, restauración de backups y continuidad del servicio.

## 7. Tareas del proyecto  
**Documento:** [tareas.md](tareas.md)  
Incluye el listado de tareas realizadas por cada miembro, sesiones y asignaciones.

## 8. Historial de cambios  
**Documento:** [CHANGELOG.md](CHANGELOG.md)  
Contiene las entradas de cada sesión del proyecto, incluyendo el cambio de alcance de la Sesión 4.

---

# Estado del proyecto

Todas las sesiones del proyecto han sido completadas:

- Sesión 1: Análisis  
- Sesión 2: Diseño  
- Sesión 3: Integración y resolución de conflictos con rebase  
- Sesión 4: Cambio de alcance (HAProxy), PR coordinados y merge final  

El repositorio se encuentra listo para la creación del **release v1.0**.
