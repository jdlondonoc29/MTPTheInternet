# Gestión de defectos — Mini MTP The Internet

Este documento detalla el proceso de gestión de defectos del proyecto y registra los defectos simulados encontrados durante la ejecución de las pruebas sobre el SUT (the-internet.herokuapp.com).

## Flujo de ciclo de vida del defecto

```
Nuevo → En proceso → Corregido → Cerrado
```

- **Nuevo:** el defecto fue identificado y documentado, aún sin asignar.
- **En proceso:** alguien del equipo está analizando o corrigiendo el defecto.
- **Corregido:** el defecto fue solucionado y está pendiente de verificación.
- **Cerrado:** se verificó la corrección y el defecto no vuelve a reproducirse.

## Severidades

| Severidad | Descripción |
|-----------|-------------|
| Crítico | Bloquea una funcionalidad esencial del sistema, sin solución alterna. |
| Alto | Afecta una funcionalidad importante; existe solución alterna limitada. |
| Medio | Afecta una funcionalidad secundaria o de forma parcial. |
| Bajo | Problema cosmético o de bajo impacto en la operación del sistema. |

## Prioridades

| Prioridad | Descripción |
|-----------|-------------|
| P0 | Hotfix — se corrige de inmediato. |
| P1 | Se corrige en el ciclo actual. |
| P2 | Se corrige cuando haya disponibilidad, sin urgencia. |

## Reglas de triage y escalación

El integrante responsable clasifica cada defecto en el momento en que lo encuentra, asignando severidad y prioridad según el impacto sobre los riesgos definidos en el MTP (sección de Riesgos). Los defectos de severidad Alta o Crítica se documentan y priorizan primero. No aplica SLA formal por tratarse de una actividad académica sobre un sandbox público de práctica.

---

## Defectos documentados

### DEF-01

| Campo | Detalle |
|---|---|
| **Descripción** | El mensaje de confirmación/error mostrado en el login (`#flash`) tiene un formato de texto inconsistente: contiene un salto de línea entre el texto del mensaje y el enlace de cierre ("×"), lo que provoca que las comparaciones de texto exacto fallen aunque el mensaje sea visualmente correcto. |
| **Pasos para reproducir** | 1) Ir a `/login`. 2) Iniciar sesión (con credenciales válidas o inválidas). 3) Inspeccionar el texto exacto del mensaje mostrado en el elemento `#flash`. |
| **Severidad** | Bajo |
| **Prioridad** | P2 |
| **Estado** | Corregido (mitigado en la automatización) |
| **Evidencia** | Fallo inicial de TC-01/TC-02 en Selenium IDE por discrepancia de texto exacto, 23/08/2026. |
| **Causa raíz** | El salto de línea entre "You logged into a secure area!" y el botón "×" impide que un patrón `glob:*texto*` haga match completo, ya que el `.` de la expresión regular generada no cruza saltos de línea. |
| **Solución aplicada** | Se reemplazó la validación por texto exacto (`assertText` + `glob`) por una verificación de contención (`assertElementPresent` con XPath `contains(., 'texto clave')`), que no depende del formato exacto del string ni de saltos de línea. |

### DEF-02

| Campo | Detalle |
|---|---|
| **Descripción** | El campo numérico de la página `/inputs` acepta valores negativos sin mostrar ninguna validación, alerta o mensaje de error. |
| **Pasos para reproducir** | 1) Ir a `/inputs`. 2) Escribir un valor negativo, por ejemplo `-5`. 3) Observar que el campo lo acepta sin ninguna advertencia. |
| **Severidad** | Medio |
| **Prioridad** | P1 |
| **Estado** | Nuevo |
| **Evidencia** | Verificación manual del equipo, 23/08/2026. |
| **Impacto** | Si este campo alimenta datos operativos reales del portal (p. ej. horas trabajadas o cantidades), permitir negativos sin validar puede corromper reportes o cálculos posteriores. Está directamente conectado a los riesgos R1/R2 del MTP. |

---

## Resumen de defectos por severidad

| Severidad | Cantidad | IDs |
|-----------|----------|-----|
| Alto | 0 | — |
| Medio | 1 | DEF-02 |
| Bajo | 1 | DEF-01 |

Detalle completo de riesgos, casos de prueba y RTM asociados: ver `MTP_The_Internet.docx`.
