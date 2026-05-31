# 03 - Planificación del proyecto

## 1. Introducción

Este documento define la planificación temporal del proyecto de despliegue de la infraestructura web de la pyme, incluyendo las fases de análisis, diseño, instalación, operación y ampliaciones posteriores. La planificación se presenta en formato de tareas secuenciadas y dependencias, simulando un diagrama de Gantt.

## 2. Objetivos de la planificación

- Establecer una secuencia clara de tareas.
- Definir responsables y dependencias.
- Identificar puntos críticos del proyecto.
- Integrar cambios de alcance solicitados por el cliente (HAProxy).
- Facilitar el seguimiento y control del proyecto.

## 3. Fases del proyecto

El proyecto se divide en las siguientes fases principales:

1. **Análisis inicial**
2. **Diseño de la infraestructura**
3. **Planificación y preparación del entorno**
4. **Instalación y configuración**
5. **Operación y mantenimiento**
6. **Cambio de alcance: integración de HAProxy**
7. **Cierre y entrega**

---

## 4. Planificación detallada (Gantt en tabla)

### 4.1. Fase 1 – Análisis inicial

| ID | Tarea | Responsable | Duración | Dependencias |
|----|--------|-------------|----------|--------------|
| A1 | Revisión de requisitos | Ambos | 0,5 días | — |
| A2 | Identificación de componentes | Ambos | 0,5 días | A1 |
| A3 | Documentación del análisis | Miembro A | 1 día | A2 |

---

### 4.2. Fase 2 – Diseño de la infraestructura

| ID | Tarea | Responsable | Duración | Dependencias |
|----|--------|-------------|----------|--------------|
| D1 | Diseño lógico inicial | Miembro A | 1 día | A3 |
| D2 | Diseño de red y seguridad | Miembro A | 1 día | D1 |
| D3 | Diseño de monitorización y backups | Miembro A | 0,5 días | D2 |
| D4 | Redacción del documento de diseño | Miembro A | 0,5 días | D3 |

---

### 4.3. Fase 3 – Preparación del entorno

| ID | Tarea | Responsable | Duración | Dependencias |
|----|--------|-------------|----------|--------------|
| P1 | Configuración del repositorio GitHub | Ambos | 0,5 días | D4 |
| P2 | Definición de ramas y flujo Git | Ambos | 0,5 días | P1 |
| P3 | Preparación del servidor base | Miembro B | 1 día | P2 |

---

### 4.4. Fase 4 – Instalación y configuración

| ID | Tarea | Responsable | Duración | Dependencias |
|----|--------|-------------|----------|--------------|
| I1 | Instalación de Apache | Miembro B | 0,5 días | P3 |
| I2 | Instalación de MySQL/MariaDB | Miembro B | 0,5 días | P3 |
| I3 | Configuración de firewall | Miembro B | 0,5 días | I1 |
| I4 | Configuración de monitorización | Miembro B | 0,5 días | I2 |
| I5 | Configuración de backups | Miembro B | 0,5 días | I2 |

---

### 4.5. Fase 5 – Operación y mantenimiento

| ID | Tarea | Responsable | Duración | Dependencias |
|----|--------|-------------|----------|--------------|
| O1 | Redacción de guía de operación | Miembro B | 1 día | I5 |
| O2 | Redacción de guía de recuperación | Miembro B | 1 día | O1 |

---

## 5. Cambio de alcance: integración de balanceador HAProxy

El cliente solicita añadir un balanceador HAProxy delante del servidor Apache. Este cambio afecta tanto al diseño como a la planificación.

### 5.1. Tareas añadidas al Gantt

| ID | Tarea | Responsable | Duración | Dependencias |
|----|--------|-------------|----------|--------------|
| H1 | Actualizar diseño para incluir HAProxy (diagrama y componentes) | Miembro A | 1 día | D4 |
| H2 | Actualizar planificación (Gantt) con nuevas tareas | Miembro A | 0,5 días | H1 |
| H3 | Crear rama `feature/balanceador-diseno` y documentar cambios | Miembro A | 0,5 días | H1 |
| H4 | Actualizar `servidor-web.md` con configuración del balanceador | Miembro B | 1 día | H1 |
| H5 | Actualizar `05-operacion.md` con tareas de mantenimiento del balanceador | Miembro B | 0,5 días | H4 |
| H6 | Crear rama `feature/balanceador-config` y documentar cambios | Miembro B | 0,5 días | H4 |
| H7 | PR de diseño (A) y revisión por B | Ambos | 0,5 días | H3 |
| H8 | PR de configuración (B) y revisión por A | Ambos | 0,5 días | H6 |
| H9 | Rebase de B si hay cambios en `main` | Miembro B | 0,5 días | H7 |
| H10 | Merge final de ambas ramas | Ambos | 0,5 días | H8, H9 |

### 5.2. Impacto en la planificación

La integración de HAProxy añade aproximadamente **3–4 días** al proyecto, pero mejora:

- Disponibilidad del servicio.
- Escalabilidad futura.
- Robustez de la arquitectura.

---

## 6. Riesgos identificados

- Retrasos si surgen conflictos en Git durante los PR.
- Posibles incompatibilidades entre HAProxy y Apache si no se configura correctamente.
- Riesgo de sobrecarga si no se ajustan los health checks del balanceador.

---

## 7. Conclusión

La planificación establece un marco claro para el desarrollo del proyecto, incluyendo el cambio de alcance solicitado por el cliente. El cronograma permite un seguimiento preciso y facilita la coordinación entre los miembros del equipo.
