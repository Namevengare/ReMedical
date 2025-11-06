# Herramientas para Reporte y Seguimiento de Requisitos - Jira

## 1. Introducción a Jira

**Jira** es una plataforma de gestión de proyectos desarrollada por Atlassian, líder en herramientas de seguimiento de requisitos, issues y desarrollo ágil.

### ¿Por Qué Jira para ReMedical?

| Necesidad | Solución en Jira |
|-----------|------------------|
| Rastrear requisitos de FDA | Issues con campos personalizados de compliance |
| Gestionar historias de usuario | Backlog con estimaciones y priorización |
| Coordinar equipo distribuido | Dashboards en tiempo real, notificaciones |
| Trazabilidad requisito→código→test | Integración con GitLab/GitHub, TestRail |
| Reportes para stakeholders | Reportes automáticos, gráficos burndown |
| Auditorías de calidad | Historial completo de cambios, comentarios |

### Alternativas a Jira

| Herramienta | Fortalezas | Debilidades |
|-------------|------------|-------------|
| **Azure DevOps** | Integración Microsoft, CI/CD robusto | Curva de aprendizaje alta |
| **Linear** | UI moderna, velocidad | Menos features empresariales |
| **Asana** | Simplicidad, colaboración | No orientado a desarrollo |
| **Monday.com** | Personalización extrema | Costo alto |
| **ClickUp** | Todo-en-uno | Puede ser abrumador |
| **GitHub Projects** | Gratis, integrado con código | Features limitados |

---

## 2. Configuración de Jira para ReMedical

### 2.1 Estructura de Proyecto

```
PROYECTO: REMEDICAL
│
├── EPIC 1: Plataforma de IA para Predicción de Diabetes
│   ├── STORY: REMED-101 - Dashboard de predicción para médicos
│   ├── STORY: REMED-102 - Modelo ML de predicción
│   ├── STORY: REMED-103 - Integración con EHR
│   └── TASK: REMED-104 - Configurar infraestructura AWS
│
├── EPIC 2: Sistema de Desarrollo de Compuestos Químicos
│   ├── STORY: REMED-201 - Simulación molecular (docking)
│   ├── STORY: REMED-202 - Biblioteca de compuestos
│   └── BUG: REMED-203 - Error en cálculo de afinidad
│
├── EPIC 3: Gestión de Datos de Pacientes (Big Data)
│   ├── STORY: REMED-301 - Pipeline ETL para datos de wearables
│   ├── STORY: REMED-302 - Data lake en AWS S3
│   └── SUBTASK: REMED-303 - Configurar Apache Spark
│
└── EPIC 4: Cumplimiento Regulatorio (FDA/HIPAA)
    ├── STORY: REMED-401 - Sistema de auditoría de acceso
    ├── STORY: REMED-402 - Encriptación de datos en reposo
    └── COMPLIANCE: REMED-403 - Documentación 21 CFR Part 11
```

### 2.2 Tipos de Issues (Issue Types)

#### Epic (Épica)
**Definición**: Iniciativa grande que se divide en múltiples historias de usuario.

**Ejemplo**:
```
EPIC: REMED-E1
Título: Plataforma de IA para Predicción de Diabetes
Descripción: Sistema completo que permita a médicos predecir riesgo de 
diabetes tipo 2 usando machine learning sobre datos de pacientes.

Objetivos de Negocio:
- Reducir incidencia de diabetes en 20%
- Aumentar eficiencia diagnóstica en 40%
- Generar $2M en revenue en el primer año

Stakeholders:
- Dr. María González (Endocrinóloga líder)
- Pacientes diabéticos (500K usuarios proyectados)
- Aseguradoras de salud

KPIs:
- Precisión modelo: >90%
- Tiempo de respuesta: <3 seg
- Adopción por médicos: >60% en 6 meses
```

#### Story (Historia de Usuario)
**Definición**: Funcionalidad desde perspectiva del usuario.

**Formato**:
```
STORY: REMED-101
Título: Dashboard de predicción de riesgo de diabetes

Como: Médico endocrinólogo
Quiero: Ver predicción de riesgo de diabetes de un paciente en un dashboard
Para: Tomar decisiones informadas sobre tratamiento preventivo

Criterios de Aceptación:
✓ Predicción muestra porcentaje de riesgo (0-100%)
✓ Gráfico de factores contribuyentes (peso: IMC 35%, glucosa 25%...)
✓ Historial de predicciones anteriores (últimos 6 meses)
✓ Botón "Generar plan de prevención" automático
✓ Exportar reporte en PDF
✓ Tiempo de carga < 3 segundos

Estimación: 13 Story Points
Prioridad: Alta
Sprint: Sprint 5
Asignado: Juan Pérez (Frontend), Ana López (Backend)
```

#### Task (Tarea)
**Definición**: Trabajo técnico sin narrativa de usuario.

**Ejemplo**:
```
TASK: REMED-104
Título: Configurar infraestructura AWS para modelo ML

Descripción:
- Provisionar instancias EC2 p3.2xlarge (GPU)
- Configurar S3 buckets para datasets (train/test/validation)
- Setup de SageMaker para entrenamiento
- Configurar CloudWatch para monitoreo

Criterios de Completitud:
✓ Instancias EC2 levantadas y accesibles
✓ Buckets S3 creados con políticas de acceso
✓ SageMaker notebook funcional
✓ Métricas visibles en CloudWatch

Estimación: 5 Story Points
Asignado: Carlos Ramírez (DevOps)
```

#### Bug (Error)
**Definición**: Defecto en funcionalidad existente.

**Ejemplo**:
```
BUG: REMED-203
Título: Error en cálculo de afinidad de unión proteína-ligando

Severidad: Alta
Prioridad: Crítica
Ambiente: Producción

Pasos para Reproducir:
1. Cargar proteína 1ABC.pdb
2. Cargar ligando aspirin.mol2
3. Ejecutar simulación de docking
4. Ver resultado de scoring

Resultado Esperado:
Afinidad de -7.5 kcal/mol (según literatura científica)

Resultado Actual:
Afinidad de -2.1 kcal/mol (inconsistente)

Logs:
[ERROR] 2025-11-05 14:32:11 - docking.py:234 - ValueError: Invalid grid dimensions

Impacto:
- Afecta validación de 150 compuestos candidatos
- Bloqueante para publicación científica
- Riesgo de decisiones incorrectas en I+D

Asignado: Dr. Patricia Morales (Computational Chemistry)
```

#### Sub-task (Subtarea)
**Definición**: Descomposición técnica de una historia.

**Ejemplo**:
```
SUB-TASK: REMED-102.1
Parent: REMED-102 (Modelo ML de predicción)
Título: Feature engineering para variables de entrada

Checklist:
□ Crear feature: ratio glucosa/edad
□ Crear feature: IMC categórico (<18.5, 18.5-25, 25-30, >30)
□ One-hot encoding para etnia
□ Normalizar variables continuas (StandardScaler)
□ Detectar y tratar outliers (IQR method)
□ Crear interacciones: edad*IMC, glucosa*triglicéridos
□ Guardar pipeline de transformación (pickle)

Estimación: 3 Story Points
Asignado: Laura Fernández (Data Scientist)
```

#### Tipos Personalizados para ReMedical

**COMPLIANCE** (Cumplimiento Regulatorio):
```
COMPLIANCE: REMED-403
Título: Documentación 21 CFR Part 11 - Registros Electrónicos

Regulación: FDA 21 CFR Part 11
Fecha Límite: 2025-12-31
Responsable: Gerardo Sánchez (Quality Assurance)

Requisitos:
□ Sistema de firma electrónica validado
□ Audit trails inalterables
□ Controles de acceso documentados
□ Procedimientos de respaldo/recuperación
□ Validación del sistema (IQ/OQ/PQ)

Evidencias Requeridas:
- Plan de validación aprobado
- Protocolos de prueba ejecutados
- Informe de validación firmado
- SOP (Standard Operating Procedures)

Estado: En Revisión Legal
```

**SPIKE** (Investigación Técnica):
```
SPIKE: REMED-305
Título: Evaluar PostgreSQL vs Cassandra para time-series de wearables

Pregunta de Investigación:
¿Qué base de datos ofrece mejor rendimiento para 10M registros/día 
de datos de glucómetros continuos (CGM)?

Criterios de Evaluación:
- Throughput de escritura (registros/seg)
- Latencia de queries (P95, P99)
- Costo de infraestructura ($/mes)
- Complejidad operacional
- Soporte para agregaciones temporales

Experimentos:
1. Benchmark escritura: 100K inserts
2. Benchmark lectura: queries de últimas 24h de 1000 pacientes
3. Prueba de recuperación ante falla
4. Estimación de costo AWS (RDS vs Keyspaces)

Time-box: 3 días
Asignado: Equipo de Data Engineering

Resultado Esperado:
Documento con recomendación fundamentada + POC ejecutable
```

---

## 3. Workflow (Flujo de Trabajo) en Jira

### 3.1 Workflow Estándar de Scrum

```
┌──────────┐      ┌──────────┐      ┌──────────┐      ┌──────────┐      ┌──────────┐
│ BACKLOG  │─────▶│   TODO   │─────▶│IN PROGRESS│─────▶│IN REVIEW │─────▶│  DONE    │
│          │      │          │      │          │      │          │      │          │
└──────────┘      └──────────┘      └──────────┘      └──────────┘      └──────────┘
                         │                │                  │                │
                         │                │                  │                │
                         │                ▼                  │                │
                         │          ┌──────────┐            │                │
                         │          │ BLOCKED  │            │                │
                         │          └──────────┘            │                │
                         │                │                  │                │
                         │                └──────────────────┘                │
                         │                                                    │
                         └────────────────────────────────────────────────────┘
                                         (Reopen)
```

**Estados Detallados**:

| Estado | Descripción | Responsable | Triggers |
|--------|-------------|-------------|----------|
| **Backlog** | Requisito identificado, pendiente de priorización | Product Owner | Creación del issue |
| **TODO** | Priorizado para sprint actual | Equipo Dev | Sprint Planning |
| **In Progress** | Desarrollo activo | Developer asignado | Inicio de trabajo |
| **Blocked** | Impedimento externo | Developer + Scrum Master | Aparece bloqueador |
| **In Review** | Code review / QA testing | Reviewer / QA | Pull Request creado |
| **Done** | Cumple Definition of Done | Product Owner | Aceptación en Sprint Review |

### 3.2 Workflow Personalizado para ReMedical

Para proyectos de salud regulados, necesitamos pasos adicionales:

```
BACKLOG → TODO → IN PROGRESS → CODE REVIEW → QA TESTING → 
MEDICAL VALIDATION → REGULATORY REVIEW → UAT → DONE
```

**Pasos Adicionales**:

**Medical Validation**:
- Panel de médicos revisa funcionalidad clínica
- Valida precisión de algoritmos médicos
- Aprueba terminología y UX para contexto hospitalario

**Regulatory Review**:
- Equipo legal verifica cumplimiento FDA/HIPAA
- Revisa documentación de trazabilidad
- Aprueba para despliegue en entornos productivos

---

## 4. Campos Personalizados (Custom Fields)

### 4.1 Campos Específicos de ReMedical

```
┌─────────────────────────────────────────────────────┐
│ ISSUE: REMED-101                                    │
├─────────────────────────────────────────────────────┤
│ Campos Estándar:                                    │
│ - Título: Dashboard de predicción de diabetes      │
│ - Tipo: Story                                       │
│ - Estado: In Progress                               │
│ - Prioridad: High                                   │
│ - Asignado: Juan Pérez                              │
│ - Sprint: Sprint 5                                  │
│ - Story Points: 13                                  │
│                                                     │
│ Campos Personalizados - ReMedical:                 │
│ ┌─────────────────────────────────────────────┐   │
│ │ 🏥 Validación Médica Requerida: Sí          │   │
│ │ 📋 Impacto Regulatorio: FDA Class II        │   │
│ │ 🔒 Nivel de Privacidad: PHI (HIPAA)         │   │
│ │ 🎯 Métrica de Éxito: Adoption rate >60%     │   │
│ │ 🧪 Test Coverage Requerido: >85%            │   │
│ │ 📊 Dataset Requerido: Diabetes_2023 (50K)   │   │
│ │ 🔬 Revisión Científica: Dr. González        │   │
│ │ 📄 Documento SOP: SOP-AI-001 v2.1           │   │
│ │ ⚠️ Nivel de Riesgo Clínico: Medio           │   │
│ │ 🌍 Mercados Objetivo: US, EU, LATAM         │   │
│ └─────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────┘
```

### 4.2 Configuración de Campos

**Ejemplo: Campo "Nivel de Riesgo Clínico"**

```
Nombre: Clinical Risk Level
Tipo: Select List (single choice)
Opciones:
  - Low (Verde): Feature sin impacto en decisiones clínicas
  - Medium (Amarillo): Afecta recomendaciones, requiere revisión médica
  - High (Rojo): Impacta directamente en salud del paciente, requiere validación exhaustiva
  - Critical (Rojo Oscuro): Riesgo de vida, requiere aprobación FDA previa

Reglas Automáticas:
- Si "High" o "Critical" → Asignar automáticamente a QA Senior
- Si "Critical" → Notificar a Medical Director
- Si "Clinical Risk Level" vacío y Epic = "Plataforma IA" → Bloquear transición a "In Progress"
```

---

## 5. Gestión del Backlog

### 5.1 Priorización con MoSCoW

Clasificar historias de usuario en:

| Categoría | Significado | Ejemplo ReMedical |
|-----------|-------------|-------------------|
| **Must Have** | Crítico para MVP | Predicción básica de diabetes, autenticación de usuarios |
| **Should Have** | Importante, pero no bloqueante | Dashboard con gráficos avanzados, exportación PDF |
| **Could Have** | Deseable si hay tiempo | Integración con Apple Health, modo oscuro |
| **Won't Have** | Fuera de scope actual | App móvil nativa, soporte 20 idiomas |

**Visualización en Jira**:
```
Backlog ReMedical - Sprint 6

🔴 MUST HAVE (Story Points: 34)
├── REMED-101 - Dashboard predicción (13 pts) [In Progress]
├── REMED-102 - Modelo ML (21 pts) [TODO]

🟡 SHOULD HAVE (Story Points: 21)
├── REMED-105 - Gráficos avanzados (8 pts) [TODO]
├── REMED-106 - Exportación PDF (13 pts) [Backlog]

🟢 COULD HAVE (Story Points: 13)
├── REMED-110 - Integración Apple Health (13 pts) [Backlog]

⚪ WON'T HAVE (Moved to Future Sprints)
├── REMED-150 - App móvil iOS/Android [Backlog]
```

### 5.2 Técnica: Weighted Shortest Job First (WSJF)

Priorización basada en valor de negocio / esfuerzo.

**Fórmula**:
```
WSJF = (Business Value + Time Criticality + Risk Reduction) / Job Size

Business Value (1-10): Impacto en revenue, usuarios, satisfacción
Time Criticality (1-10): Urgencia (deadlines, dependencias)
Risk Reduction (1-10): Mitigación de riesgos técnicos/negocio
Job Size (1-20): Story Points
```

**Ejemplo**:
```
REMED-101: Dashboard Predicción
- Business Value: 9 (core feature)
- Time Criticality: 8 (demo a inversores en 3 semanas)
- Risk Reduction: 7 (valida viabilidad técnica)
- Job Size: 13 Story Points
→ WSJF = (9 + 8 + 7) / 13 = 1.85

REMED-110: Integración Apple Health
- Business Value: 4 (nice to have)
- Time Criticality: 2 (no urgente)
- Risk Reduction: 3 (bajo riesgo)
- Job Size: 13 Story Points
→ WSJF = (4 + 2 + 3) / 13 = 0.69

Conclusión: Priorizar REMED-101 (1.85) sobre REMED-110 (0.69)
```

---

## 6. Sprint Planning en Jira

### 6.1 Capacidad del Equipo

**Cálculo de Velocity**:
```
Velocity = Promedio de Story Points completados en últimos 3 sprints

Ejemplo ReMedical:
Sprint 3: 34 SP
Sprint 4: 29 SP
Sprint 5: 38 SP
→ Velocity = (34 + 29 + 38) / 3 = 33.67 ≈ 34 SP

Para Sprint 6, comprometer máximo 34 Story Points
```

**Capacidad Individual** (considerando días festivos, vacaciones):
```
Equipo ReMedical - Sprint 6 (2 semanas)

Developer          Días Disponibles   Capacidad (SP/día)   Total SP
─────────────────────────────────────────────────────────────────────
Juan Pérez         10                 2.5                  25
Ana López          8 (2 días festivos) 3.0                  24
Carlos Ramírez     10                 2.0                  20
Laura Fernández    6 (4 días vacaciones) 3.5                21
─────────────────────────────────────────────────────────────────────
TOTAL EQUIPO                                               90 SP

Pero: Velocity histórico = 34 SP
Conclusión: Hay subutilización o overestimation
→ Acción: Revisar estimaciones o identificar impedimentos
```

### 6.2 Sprint Board

```
┌────────────────────────────────────────────────────────────────────┐
│ SPRINT 6: "Diabetes Prediction MVP" (Nov 5 - Nov 18, 2025)        │
├────────────────────────────────────────────────────────────────────┤
│ TODO (21 SP) │ IN PROGRESS (13 SP) │ IN REVIEW (8 SP) │ DONE (0 SP)│
├──────────────┼─────────────────────┼──────────────────┼────────────┤
│ REMED-102    │ REMED-101           │ REMED-99         │            │
│ Modelo ML    │ Dashboard UI        │ Auth system      │            │
│ 21 SP        │ 13 SP               │ 8 SP             │            │
│ [Ana López]  │ [Juan Pérez]        │ [Carlos Ramírez] │            │
│              │                     │                  │            │
│              │                     │                  │            │
│              │                     │                  │            │
└──────────────┴─────────────────────┴──────────────────┴────────────┘

Progreso: 8 SP / 42 SP completados (19%)
Burndown: On track ✓
Impediments: 0
```

---

## 7. Reportes y Métricas en Jira

### 7.1 Burndown Chart

Muestra trabajo restante vs tiempo en el sprint.

```
Story Points
│
40│     ●
  │      ╲
35│       ●
  │        ╲
30│         ●── Ideal
  │          ╲
25│           ○── Real
  │          ╱ ╲
20│         ●   ○
  │              ╲
15│               ●
  │                ╲
10│                 ●
  │                  ╲
5 │                   ●
  │                    ╲
0 │─────────────────────●
  └─┬──┬──┬──┬──┬──┬──┬──┬──┬──┬──
    D1 D2 D3 D4 D5 D6 D7 D8 D9 D10
                      (Días del Sprint)

Análisis:
- Días 1-3: Adelantados al plan ✓
- Días 4-6: Retraso (Ana de vacaciones)
- Días 7-10: Recuperación, finalización on-time
```

### 7.2 Velocity Chart

Compara Story Points comprometidos vs completados por sprint.

```
Story Points
│
50│         ┌──┐
  │         │  │ Committed: 42 SP
45│         │  │
  │    ┌──┐ │  │ Completed: 34 SP
40│    │  │ │  │
  │    │  │ │  │
35│    │  │ │  │┌──┐
  │    │  │ │  ││  │
30│ ┌──┤  │ │  ││  │
  │ │  │  │ │  ││  │
25│ │  │  │ │  ││  │
  │ │  │  │ │  ││  │
20│ │  │  │ │  ││  │
  │ │  │  │ │  ││  │
15│ │  │  │ │  ││  │
  │ │  │  │ │  ││  │
10│ │  │  │ │  ││  │
  │ │  │  │ │  ││  │
5 │ │  │  │ │  ││  │
  │ │  │  │ │  ││  │
0 │─┴──┴──┴──┴──┴─┴──┴─
  └─Sprint Sprint Sprint Sprint
      3     4     5     6

Insights:
- Sprint 5: Overcommitment (42 comprometidos, 34 completados)
- Velocity promedio: 30-34 SP
- Recomendación: Comprometer máximo 35 SP en Sprint 7
```

### 7.3 Cumulative Flow Diagram (CFD)

Visualiza distribución de trabajo en cada estado a lo largo del tiempo.

```
Issues
│
60│                                    ╱── Done
  │                               ╱───
50│                          ╱────
  │                     ╱────
40│                ╱────          ╱── In Review
  │           ╱────          ╱───
30│      ╱────          ╱────      ╱── In Progress
  │ ╱────          ╱────      ╱───
20│          ╱────      ╱────       ╱── TODO
  │     ╱────      ╱────       ╱───
10│╱────      ╱────       ╱────
  │      ╱────       ╱────
0 │──────────────────────────────────
  └─W1──W2──W3──W4──W5──W6──W7──W8──
                    (Semanas)

Análisis:
- Semana 4: Cuello de botella en "In Review" (banda ancha)
  → Acción: Agregar más reviewers
- Semana 6-7: Flujo constante (bandas paralelas) ✓
```

### 7.4 Control Chart

Detecta variabilidad en tiempo de ciclo (cycle time).

```
Días
│
20│                           ●  ← Outlier (investigar)
  │
15│              ●
  │        ●           ●
10│  ●        ●    ●       ●  ●
  │     ●  ●    ●    ●  ●     ●
5 │  ●  ●     ●   ●   ●   ●  ●  ●
  │─────────────────────────────────── Media: 7 días
0 │
  └─REMED─────────────────────────────▶
     -99 -100 -101 -102 -103 -104

Control Limits:
- Upper Control Limit (UCL): 15 días
- Lower Control Limit (LCL): 2 días
- Promedio: 7 días

Issue REMED-103 (20 días): Investigar causa raíz
→ Descubrimiento: Esperando aprobación FDA (externa)
→ Acción: Crear estado "Waiting External Approval"
```

---

## 8. Integraciones con Otras Herramientas

### 8.1 Jira + Confluence (Documentación)

**Uso**: Vincular especificaciones técnicas detalladas.

```
STORY: REMED-101

📄 Confluence Pages:
┌─────────────────────────────────────────────────┐
│ [Confluence] Especificación Técnica Dashboard   │
│ https://remedical.atlassian.net/wiki/SPEC-101   │
│                                                 │
│ Contenido:                                      │
│ - Arquitectura de componentes (React)          │
│ - API endpoints consumidos                     │
│ - Esquema de base de datos                     │
│ - Mockups de UI (Figma embebidos)              │
│ - Decisiones de diseño (ADRs)                  │
└─────────────────────────────────────────────────┘
```

### 8.2 Jira + GitHub/GitLab (Control de Versiones)

**Uso**: Trazabilidad requisito→código.

```
Commit Message:
git commit -m "REMED-101: Add diabetes risk prediction dashboard

- Implement React components: RiskGauge, FactorsChart
- Connect to ML API endpoint /api/v1/predict
- Add unit tests (coverage 87%)
- Update Storybook stories

Closes REMED-101"
```

**En Jira, automáticamente aparece**:
```
REMED-101
├── 📂 Development
│   ├── Branch: feature/REMED-101-dashboard
│   ├── Commits: 12
│   ├── Pull Request: #234 (Merged)
│   └── Builds: ✓ Passed (CI/CD)
└── 🧪 Test Results
    ├── Unit Tests: 45 passed
    ├── Integration Tests: 12 passed
    └── Coverage: 87%
```

### 8.3 Jira + Slack (Comunicación)

**Configuración de Notificaciones**:
```
Canal: #remedial-dev

Notificaciones automáticas:
- Issue creado con prioridad "Critical" → @channel
- Sprint iniciado → Mensaje con objetivos
- Issue bloqueado >2 días → Notificar a Scrum Master
- Build falló en CI/CD → Notificar a autor del commit
- PR listo para review → Notificar a reviewers asignados

Ejemplo de mensaje:
──────────────────────────────────────
🚨 [JIRA] REMED-203 (BUG) - BLOQUEADO

Título: Error en cálculo de afinidad
Asignado: @patricia.morales
Bloqueado por: Falta acceso a servidor de simulación

🔗 https://remedical.atlassian.net/browse/REMED-203
──────────────────────────────────────
```

### 8.4 Jira + TestRail (Gestión de Pruebas)

**Uso**: Vincular casos de prueba con requisitos.

```
STORY: REMED-101

🧪 TestRail Test Cases:
┌──────────────────────────────────────────────────┐
│ TC-101.1: Verify risk prediction display        │
│ Status: ✓ Passed                                 │
│                                                  │
│ TC-101.2: Verify factors chart rendering        │
│ Status: ✓ Passed                                 │
│                                                  │
│ TC-101.3: Verify performance <3 seconds          │
│ Status: ✗ Failed (actual: 4.2s)                  │
│ Bug Created: REMED-108                           │
│                                                  │
│ TC-101.4: Verify PDF export functionality        │
│ Status: ⚠ Blocked (waiting for library upgrade)  │
└──────────────────────────────────────────────────┘

Test Coverage: 75% (3/4 passed)
```

---

## 9. Automatizaciones en Jira

### 9.1 Reglas de Automatización

**Ejemplo 1: Auto-asignar Issues Críticos**
```
TRIGGER: Issue creado
CONDITIONS: 
  - Prioridad = "Critical"
  - Tipo = "Bug"
ACTIONS:
  - Asignar a: QA Lead (María García)
  - Enviar notificación a: CTO
  - Agregar etiqueta: "hotfix"
  - Transicionar a: "In Progress"
```

**Ejemplo 2: Recordatorio de Issues Estancados**
```
TRIGGER: Scheduled (Diariamente a las 9:00 AM)
CONDITIONS:
  - Estado = "In Progress"
  - Última actualización > 3 días atrás
  - Asignado no es null
ACTIONS:
  - Comentar: "@assignee Este issue no tiene actividad en 3+ días. 
              ¿Hay algún impedimento?"
  - Notificar a: Scrum Master
```

**Ejemplo 3: Validación de Campos Requeridos**
```
TRIGGER: Issue transicionado a "In Review"
CONDITIONS:
  - Campo "Test Coverage" está vacío
ACTIONS:
  - Bloquear transición
  - Mostrar mensaje: "Debe especificar Test Coverage antes de pasar a Review"
```

### 9.2 JQL (Jira Query Language)

**Queries Útiles para ReMedical**:

```sql
-- Issues críticos sin asignar
project = REMEDICAL AND priority = Critical AND assignee is EMPTY

-- Bugs en producción
project = REMEDICAL AND type = Bug AND status != Done 
  AND labels = "production"

-- Historias pendientes de validación médica
project = REMEDICAL AND type = Story 
  AND "Medical Validation Required" = Yes 
  AND "Medical Validation Status" != Approved

-- Work in progress por persona
project = REMEDICAL AND status = "In Progress" 
  AND assignee = currentUser()

-- Story Points completados en Sprint 6
project = REMEDICAL AND sprint = "Sprint 6" 
  AND status = Done AND type in (Story, Task)

-- Issues bloqueados por más de 2 días
project = REMEDICAL AND status = Blocked 
  AND status changed to Blocked before -2d

-- Requisitos de cumplimiento FDA pendientes
project = REMEDICAL AND "Regulatory Impact" ~ "FDA" 
  AND status != Done AND labels = "compliance"
```

---

## 10. Mejores Prácticas

### ✅ DOs

1. **Escribir criterios de aceptación claros**
   ```
   ❌ Malo: "El dashboard debe ser rápido"
   ✅ Bueno: "El dashboard debe cargar en <3 segundos con 1000 pacientes"
   ```

2. **Mantener issues atómicos**
   - Una historia = una funcionalidad
   - Si historia >20 SP, dividir en sub-stories

3. **Actualizar estado diariamente**
   - Evita "zombie issues" (parecen activos pero están abandonados)

4. **Agregar comentarios con contexto**
   ```
   ❌ Malo: "No funciona"
   ✅ Bueno: "Error al cargar datos con >5000 registros. 
              Ver screenshot adjunto. Logs: server.log línea 234"
   ```

5. **Usar etiquetas (labels) consistentemente**
   ```
   - backend / frontend / devops / ml
   - bug / feature / improvement
   - production / staging
   - compliance / security
   ```

### ❌ DON'Ts

1. **No crear issues duplicados**
   - Buscar primero con JQL antes de crear

2. **No dejar issues huérfanos**
   - Todo issue debe estar en un Epic o tener justificación

3. **No cambiar estimaciones sin documentar**
   - Si original 5 SP → actual 13 SP, explicar en comentarios

4. **No usar Jira como chat**
   - Conversaciones →Slack
   - Decisiones técnicas → Confluence
   - Jira → tracking de estado

5. **No ignorar Definition of Done**
   ```
   DoD para Stories en ReMedical:
   ✓ Código en main branch
   ✓ Tests automatizados (cobertura >80%)
   ✓ Code review aprobado
   ✓ QA testing passed
   ✓ Documentación técnica actualizada
   ✓ Demo aceptado por Product Owner
   ✓ Si aplica: Validación médica aprobada
   ```

---

## 11. Dashboard Ejecutivo en Jira

**Para Stakeholders No Técnicos**:

```
┌─────────────────────────────────────────────────────────┐
│          ReMedical - Executive Dashboard                 │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  📊 Sprint Progress                                     │
│  ════════════════════════════════════════════          │
│  Sprint 6: 19 SP / 42 SP (45%)      [══════────────]   │
│  Projected Completion: On Track ✓                       │
│                                                         │
│  🎯 Epic Status                                         │
│  ┌───────────────────────────────────────────────┐    │
│  │ Epic 1: Plataforma IA Diabetes                │    │
│  │ Progress: 67% │ At Risk: 0 │ On Track: 8     │    │
│  ├───────────────────────────────────────────────┤    │
│  │ Epic 2: Sistema Compuestos Químicos           │    │
│  │ Progress: 34% │ At Risk: 2 │ On Track: 5     │    │
│  └───────────────────────────────────────────────┘    │
│                                                         │
│  🚨 Critical Issues                                     │
│  ┌─────────────────────────────────────────────┐      │
│  │ REMED-203: Error cálculo afinidad           │      │
│  │ Bloqueado hace 5 días | Asignado: Patricia  │      │
│  └─────────────────────────────────────────────┘      │
│                                                         │
│  📈 Key Metrics                                         │
│  - Velocity: 34 SP/sprint (promedio últimos 3)         │
│  - Bugs en Producción: 2 (Severidad: Alta)             │
│  - Test Coverage: 82% (objetivo: 85%)                  │
│  - Tech Debt Issues: 12 (total 45 SP)                  │
│                                                         │
│  🗓 Upcoming Milestones                                 │
│  - Nov 18: Sprint 6 Review                              │
│  - Nov 25: MVP Demo to Investors                        │
│  - Dec 15: FDA Documentation Submission                 │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## Referencias

- Atlassian. (2024). Jira Software Documentation. https://www.atlassian.com/software/jira/guides
- Cohn, M. (2005). Agile Estimating and Planning. Prentice Hall.
- Rubin, K. S. (2012). Essential Scrum: A Practical Guide. Addison-Wesley.
- Scaled Agile Framework (SAFe). (2024). WSJF - Weighted Shortest Job First.
