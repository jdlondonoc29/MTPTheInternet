# Mini MTP — The Internet

Proyecto de la Actividad 2 (Calidad en Software II): elaboración de un **Mini Master Test Plan (MTP)** con alcance, análisis de riesgos, estrategia de pruebas, trazabilidad, gestión de defectos y automatización mínima viable.

## Sistema bajo prueba (SUT)

- **Aplicación:** [the-internet.herokuapp.com](https://the-internet.herokuapp.com), usada como sandbox estable para representar el módulo de autenticación y captura de datos del *Portal de Colaboradores* de Andes Soluciones S.A.S.
- **Pantallas evaluadas:** Login (`/login`), Inputs (`/inputs`), Checkboxes (`/checkboxes`).

## Integrantes

- Jefferson

## Estructura del repositorio

```
├── README.md                  → Este archivo
├── MTP_The_Internet.docx/pdf  → Mini Master Test Plan completo (documento principal de la entrega)
├── DEFECTOS.md                 → Gestión de defectos: flujo, severidades y defectos documentados
├── test/
│   └── MTP_The_Internet.side  → Suite de automatización (Selenium IDE)
└── assets/
    └── evidencia_ejecucion.png → Captura de la ejecución exitosa de la suite
```

## Cómo ejecutar las pruebas automatizadas

1. Instalar la extensión **Selenium IDE** (por Selenium HQ) en Chrome o Firefox.
2. Abrir la extensión → **Open an existing project** → seleccionar `test/MTP_The_Internet.side`.
3. En la pestaña **Suites**, elegir `Suite_Regresion_Minima` y pulsar **Run all tests** (▶️).
4. Verificar que las 3 pruebas queden en verde (Passed).
5. La evidencia de la última ejecución exitosa está en `assets/evidencia_ejecucion.png`.

## Casos de prueba automatizados

| ID | Nombre | Qué valida |
|----|--------|------------|
| TC-01 | Login válido | Redirección a `/secure` y mensaje de éxito |
| TC-02 | Login con contraseña inválida | Mensaje de error correspondiente |
| TC-07 | Input numérico con texto | El campo `type="number"` no permite caracteres no numéricos |

Los demás casos diseñados (TC-03 a TC-06, TC-08) se documentan y ejecutan de forma manual — el detalle completo de los 8 casos, la matriz de trazabilidad (RTM) y el resto de secciones del plan están en `MTP_The_Internet.docx`.

## Gestión de defectos

Ver [`DEFECTOS.md`](./DEFECTOS.md) para el flujo de defectos, severidades/prioridades y el detalle de los defectos simulados encontrados (DEF-01, DEF-02).

## Control de versiones

- Repositorio: https://github.com/jdlondonoc29/MTPTheInternet
- Tag de entrega: `v1.0`
