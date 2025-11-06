# Historias de Usuario y Agilismo - ReMedical

## 1. Historias de Usuario (User Stories)

### 1.1 Definición y Propósito

Una **Historia de Usuario** es una descripción breve y simple de una funcionalidad desde la perspectiva del usuario final.

**Formato Clásico (Mike Cohn, 2004)**:
```
Como [rol de usuario]
Quiero [funcionalidad/acción]
Para [beneficio/valor de negocio]
```

**Características de una Buena Historia: INVEST**

| Letra | Significado | Descripción | Ejemplo ReMedical |
|-------|-------------|-------------|-------------------|
| **I** | Independent | Independiente de otras historias | "Predicción de diabetes" no depende de "Exportar PDF" |
| **N** | Negotiable | Abierta a discusión, no es contrato rígido | "Dashboard intuitivo" → negociar qué gráficos específicos |
| **V** | Valuable | Aporta valor al usuario/negocio | Predicción permite intervención temprana → reduce costos |
| **E** | Estimable | El equipo puede estimar esfuerzo | Con arquitectura definida, podemos estimar en SP |
| **S** | Small | Completable en un sprint (1-2 semanas) | 13 SP para dashboard es manejable en 1 sprint |
| **T** | Testable | Criterios de aceptación claros y verificables | "Predicción en <3 seg" es medible objetivamente |

---

## 2. Anatomía de una Historia de Usuario Completa

### Ejemplo: Historia para ReMedical

```
┌─────────────────────────────────────────────────────────────────────┐
│ ID: REMED-101                                   Tipo: User Story    │
│ Título: Dashboard de Predicción de Riesgo de Diabetes              │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│ 📝 NARRATIVA                                                        │
│                                                                     │
│   Como: Médico endocrinólogo                                       │
│   Quiero: Visualizar la predicción de riesgo de diabetes de un    │
│           paciente en un dashboard interactivo                     │
│   Para: Identificar pacientes de alto riesgo y recomendar         │
│         intervenciones preventivas tempranamente                   │
│                                                                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│ ✅ CRITERIOS DE ACEPTACIÓN                                          │
│                                                                     │
│   1. Dado que el médico selecciona un paciente                    │
│      Cuando el sistema calcula la predicción                       │
│      Entonces se muestra:                                          │
│      ✓ Porcentaje de riesgo (0-100%) con código de colores        │
│        - Verde (0-30%): Bajo                                       │
│        - Amarillo (31-60%): Moderado                               │
│        - Rojo (61-100%): Alto                                      │
│      ✓ Tiempo de respuesta < 3 segundos                            │
│                                                                     │
│   2. Dado que la predicción se ha calculado                        │
│      Cuando el dashboard se renderiza                              │
│      Entonces se muestran los top 5 factores contribuyentes       │
│      con su peso relativo (e.g., "IMC: 35%, Glucosa: 25%...")     │
│                                                                     │
│   3. Dado que existen predicciones históricas                      │
│      Cuando el médico accede al dashboard                          │
│      Entonces se muestra un gráfico de tendencia de los últimos   │
│      6 meses con marcadores en cada predicción                     │
│                                                                     │
│   4. Dado que el riesgo es >70%                                    │
│      Cuando la predicción se calcula                               │
│      Entonces el sistema genera automáticamente:                   │
│      ✓ Alerta visible en el dashboard (ícono ⚠️)                   │
│      ✓ Sugerencias de intervención (dieta, ejercicio, medicación) │
│                                                                     │
│   5. Dado que el médico quiere compartir el reporte               │
│      Cuando hace clic en "Exportar"                                │
│      Entonces se genera un PDF con:                                │
│      ✓ Datos del paciente (nombre, fecha)                          │
│      ✓ Resultado de predicción                                     │
│      ✓ Gráficos de factores y tendencia                            │
│      ✓ Descarga en <2 segundos                                     │
│                                                                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│ 🎯 DEFINICIÓN DE "TERMINADO" (Definition of Done)                  │
│                                                                     │
│   ☐ Código implementado y mergeado a rama main                     │
│   ☐ Unit tests escritos (cobertura >85%)                           │
│   ☐ Integration tests con mock de API ML                           │
│   ☐ Code review aprobado por 2 seniors                             │
│   ☐ QA testing manual completado (checklist de 15 items)           │
│   ☐ Performance testing: 100 requests concurrentes <3s             │
│   ☐ Responsiveness verificado (desktop, tablet, móvil)             │
│   ☐ Validación por panel de 3 médicos (usabilidad)                 │
│   ☐ Documentación técnica en Confluence                            │
│   ☐ Demo aceptado en Sprint Review por Product Owner               │
│   ☐ Deployment a staging exitoso                                   │
│   ☐ Registro de auditoría funcionando (HIPAA compliance)           │
│                                                                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│ 📊 ESTIMACIÓN Y METADATA                                            │
│                                                                     │
│   Story Points: 13                                                 │
│   Prioridad: Alta                                                  │
│   Epic: Plataforma de IA para Predicción de Diabetes              │
│   Sprint: Sprint 5                                                 │
│   Estimado por: Equipo completo (Planning Poker)                   │
│                                                                     │
│   Breakdown Técnico:                                               │
│   - Frontend (React components): 5 SP                              │
│   - Backend API (FastAPI endpoint): 3 SP                           │
│   - Integración ML model: 2 SP                                     │
│   - Testing & QA: 2 SP                                             │
│   - Documentación: 1 SP                                            │
│                                                                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│ 👥 ASIGNACIÓN                                                       │
│                                                                     │
│   Developer Frontend: Juan Pérez                                   │
│   Developer Backend: Ana López                                     │
│   QA Engineer: Roberto Sánchez                                     │
│   Medical Validator: Dr. María González                            │
│                                                                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│ 🔗 DEPENDENCIAS                                                     │
│                                                                     │
│   Bloqueado por:                                                   │
│   - REMED-102: Modelo ML de predicción (debe estar desplegado)    │
│   - REMED-095: Sistema de autenticación (para acceso seguro)      │
│                                                                     │
│   Bloquea a:                                                       │
│   - REMED-105: Gráficos avanzados de análisis                      │
│   - REMED-110: Integración con Apple Health                        │
│                                                                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│ 📎 ATTACHMENTS                                                      │
│                                                                     │
│   - mockup_dashboard_v3.png (Figma design)                         │
│   - user_flow_diagram.pdf (Flujo de interacción)                   │
│   - api_contract.yaml (OpenAPI specification)                      │
│   - medical_validation_protocol.docx                               │
│                                                                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│ 🏥 CAMPOS PERSONALIZADOS REMEDIAL                                   │
│                                                                     │
│   Validación Médica Requerida: Sí                                 │
│   Impacto Regulatorio: FDA Class II                               │
│   Nivel de Privacidad: PHI (Protected Health Information)         │
│   Test Coverage Requerido: >85%                                    │
│   Revisión Científica: Dr. González (Aprobado)                    │
│   Nivel de Riesgo Clínico: Medio                                  │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 3. Técnicas de Escritura de Historias de Usuario

### 3.1 Técnica: Job Stories (Jobs-to-be-Done)

**Formato**:
```
Cuando [situación/contexto]
Quiero [motivación]
Para [resultado esperado]
```

**Ejemplo ReMedical**:
```
❌ Historia tradicional:
Como médico
Quiero recibir alertas de pacientes de alto riesgo
Para intervenir a tiempo

✅ Job Story (más contexto):
Cuando estoy revisando mi lista de pacientes del día
Y uno de ellos ha desarrollado un riesgo alto de diabetes desde la última visita
Quiero recibir una notificación destacada al abrir su expediente
Para poder ajustar el plan de tratamiento inmediatamente en la consulta
```

**Ventaja**: Enfoca en el contexto y motivación, no en el rol.

### 3.2 Técnica: Story Mapping

Organizar historias en un mapa 2D: usuario journey (horizontal) × detalle (vertical).

```
MAPA DE HISTORIAS: Flujo de Predicción de Diabetes

Actividades (Backbone):
┌─────────────┬──────────────┬───────────────┬─────────────────┬──────────────┐
│   ACCEDER   │  SELECCIONAR │   ANALIZAR    │   INTERPRETAR   │   ACTUAR     │
│   SISTEMA   │   PACIENTE   │    DATOS      │   RESULTADOS    │              │
└─────────────┴──────────────┴───────────────┴─────────────────┴──────────────┘

Tareas (Walking Skeleton - MVP):
├─────────────┼──────────────┼───────────────┼─────────────────┼──────────────┤
│ Login con   │ Búsqueda por │ Ver datos     │ Ver predicción  │ Guardar en   │
│ SSO         │ nombre       │ del paciente  │ de riesgo       │ historial    │
└─────────────┴──────────────┴───────────────┴─────────────────┴──────────────┘

Tareas (Release 2 - Mejorado):
├─────────────┼──────────────┼───────────────┼─────────────────┼──────────────┤
│ Login con   │ Búsqueda     │ Ver gráficos  │ Ver factores    │ Generar      │
│ biométricos │ avanzada     │ de tendencia  │ contribuyentes  │ reporte PDF  │
│             │ (filtros)    │               │                 │              │
└─────────────┴──────────────┴───────────────┴─────────────────┴──────────────┘

Tareas (Release 3 - Completo):
├─────────────┼──────────────┼───────────────┼─────────────────┼──────────────┤
│ Login con   │ Búsqueda con │ Comparar con  │ Explicabilidad  │ Programar    │
│ voz         │ IA (NLP)     │ cohortes      │ IA (SHAP)       │ seguimiento  │
│             │              │ similares     │                 │ automático   │
└─────────────┴──────────────┴───────────────┴─────────────────┴──────────────┘

                              ▲
                              │
                      Prioridad decreciente
```

**Uso en Planificación**:
- **Fila 1 (MVP)**: Historias para Sprint 1-2
- **Fila 2**: Historias para Sprint 3-5
- **Fila 3**: Backlog futuro (6+ meses)

### 3.3 Técnica: Gherkin (BDD - Behavior-Driven Development)

**Formato**: Dado-Cuando-Entonces (Given-When-Then)

**Ejemplo**:
```gherkin
Feature: Predicción de Riesgo de Diabetes
  Como médico endocrinólogo
  Quiero predecir el riesgo de diabetes de mis pacientes
  Para identificar casos de alto riesgo tempranamente

  Background:
    Dado que el médico está autenticado en el sistema
    Y tiene permisos para ver datos de pacientes

  Scenario: Predicción exitosa con datos completos
    Dado que el paciente "Juan Pérez" tiene los siguientes datos:
      | Campo            | Valor  |
      | Edad             | 45     |
      | IMC              | 32.5   |
      | Glucosa ayunas   | 110    |
      | HbA1c            | 5.9    |
      | Historial familiar | Sí   |
    Cuando el médico solicita la predicción de riesgo
    Entonces el sistema debe calcular la predicción en menos de 3 segundos
    Y debe mostrar un riesgo de "72%" con clasificación "Alto" (rojo)
    Y debe mostrar los factores contribuyentes:
      | Factor             | Peso |
      | IMC elevado        | 35%  |
      | Glucosa borderline | 28%  |
      | Historial familiar | 22%  |
      | Edad               | 15%  |

  Scenario: Manejo de datos incompletos
    Dado que el paciente "Ana García" no tiene valor de HbA1c registrado
    Cuando el médico solicita la predicción de riesgo
    Entonces el sistema debe mostrar un mensaje:
      "Faltan datos requeridos: HbA1c. ¿Desea ingresar manualmente?"
    Y debe ofrecer un formulario para completar datos faltantes

  Scenario: Alerta automática para alto riesgo
    Dado que un paciente tiene una predicción de riesgo >70%
    Cuando la predicción se calcula
    Entonces el sistema debe generar una alerta visible con ícono ⚠️
    Y debe mostrar recomendaciones de intervención:
      """
      - Referir a programa de prevención de diabetes
      - Considerar metformina profiláctica
      - Programar seguimiento en 3 meses
      """
    Y debe enviar notificación al médico vía email y app móvil
```

**Ventajas**:
- Lenguaje natural entendible por todos
- Se convierte directamente en tests automatizados (Cucumber, Behave)
- Sirve como documentación ejecutable

---

## 4. Gestión Ágil de Historias de Usuario

### 4.1 El Backlog de Producto

**Estructura del Backlog en ReMedical**:

```
BACKLOG DE PRODUCTO - REMEDIAL
(Ordenado por prioridad descendente)

🔴 ALTA PRIORIDAD (Next 1-2 Sprints)
├── [34 SP] EPIC 1: Plataforma IA Predicción Diabetes
│   ├── [13 SP] REMED-101: Dashboard predicción (In Progress - Sprint 5)
│   ├── [21 SP] REMED-102: Modelo ML XGBoost (TODO - Sprint 6)
│   └── [8 SP]  REMED-103: Integración EHR (TODO - Sprint 6)
│
🟡 MEDIA PRIORIDAD (Sprints 3-5)
├── [55 SP] EPIC 2: Sistema Compuestos Químicos
│   ├── [13 SP] REMED-201: Simulación molecular
│   ├── [21 SP] REMED-202: Biblioteca de compuestos
│   └── [21 SP] REMED-203: Análisis de toxicidad
│
🟢 BAJA PRIORIDAD (6+ meses)
├── [34 SP] EPIC 4: App Móvil para Pacientes
│   ├── [13 SP] REMED-401: Onboarding y registro
│   ├── [13 SP] REMED-402: Dashboard personal de salud
│   └── [8 SP]  REMED-403: Notificaciones push
│
⚪ ICEBOX (Ideas futuras)
├── REMED-500: Integración con Apple Watch
├── REMED-501: Chatbot médico con GPT-4
└── REMED-502: Análisis de voz para detección de depresión
```

### 4.2 Refinamiento del Backlog (Grooming)

**Frecuencia**: Semanal, 1-2 horas
**Participantes**: Product Owner, Scrum Master, Equipo Dev (2-3 representantes)

**Agenda Típica**:
```
1. [15 min] Revisar historias nuevas
   - Validar formato y claridad
   - Hacer preguntas de clarificación

2. [30 min] Estimar historias del top del backlog
   - Planning Poker para sprints futuros
   - Identificar spikes técnicos necesarios

3. [15 min] Dividir historias grandes (>20 SP)
   REMED-102 (21 SP) → Dividir en:
   ├── REMED-102.1: Data preprocessing (5 SP)
   ├── REMED-102.2: Model training (8 SP)
   └── REMED-102.3: Model deployment (8 SP)

4. [30 min] Aclarar dependencias
   - REMED-103 requiere que REMED-095 (Auth) esté terminado
   - REMED-201 necesita acceso a cluster de GPU (provisionar)

5. [10 min] Reordenar por prioridad
   - Business value cambió: REMED-105 sube a Alta
```

### 4.3 Estimación con Planning Poker

**Secuencia de Fibonacci Modificada**: 1, 2, 3, 5, 8, 13, 20, 40, 100

**Proceso**:
```
1. Product Owner lee la historia REMED-102
   "Como médico quiero que el sistema prediga riesgo de diabetes..."

2. Equipo hace preguntas de clarificación
   Dev1: "¿Qué algoritmos de ML debemos probar?"
   PO: "XGBoost, Random Forest y Neural Network"
   Dev2: "¿Ya tenemos el dataset limpio?"
   PO: "Sí, 50K registros en S3"

3. Cada miembro elige una carta en secreto
   Juan (Frontend): 8 SP
   Ana (Backend): 13 SP
   Carlos (ML): 21 SP
   Laura (QA): 5 SP

4. Revelan cartas simultáneamente

5. Discuten extremos (Laura: 5 SP vs Carlos: 21 SP)
   Laura: "Pensé solo en testing del modelo"
   Carlos: "Incluye feature engineering, tuning de hiperparámetros, 
           validación cruzada, deployment..."

6. Re-estimación
   Todos: 13 SP (consenso)
   
7. PO registra en Jira: REMED-102 = 13 Story Points
```

**Referencia de Story Points en ReMedical**:
| SP | Complejidad | Ejemplo |
|----|-------------|---------|
| 1 | Trivial | Cambiar texto de botón, ajustar colores |
| 2 | Simple | Agregar validación de formulario |
| 3 | Pequeño | Crear endpoint REST simple (CRUD) |
| 5 | Mediano | Dashboard con 2-3 gráficos |
| 8 | Complejo | Integración con API externa (EHR) |
| 13 | Muy Complejo | Feature completo con backend + frontend + ML |
| 20+ | Épico | Debe dividirse en historias más pequeñas |

---

## 5. Retos en el Agilismo

### 5.1 Reto: Requisitos Cambiantes Constantemente

**Problema**:
```
Sprint 3: "Queremos predicción de diabetes"
Sprint 4: "Ahora también hipertensión"
Sprint 5: "Mejor solo diabetes pero con explicabilidad IA"
Sprint 6: "Agreguemos análisis de riesgo cardiovascular"
```

**Impacto**:
- Trabajo desperdiciado (código desechado)
- Equipo frustrado y desmotivado
- Velocity errática
- Nunca se termina nada completamente

**Soluciones**:

1. **Congelar Scope Durante el Sprint**
   ```
   ✅ Política ReMedical:
   - Sprint Planning: Se comprometen historias
   - Durante sprint: CERO cambios al sprint actual
   - Cambios urgentes → Van al backlog para próximo sprint
   - Excepción: Bugs críticos de producción
   ```

2. **Product Owner Empoderado**
   ```
   - PO tiene autoridad final sobre prioridades
   - Stakeholders externos no pueden "saltarse" al PO
   - Solicitudes → PO → Backlog → Priorización → Sprint
   ```

3. **Definir "Mínimo Producto Viable" (MVP) Claro**
   ```
   MVP ReMedical Plataforma IA:
   ✅ Predicción de diabetes tipo 2
   ✅ Dashboard básico
   ✅ Integración con 1 sistema EHR (Epic)
   ❌ Predicción de otras enfermedades
   ❌ App móvil
   ❌ Integración con 10 EHRs
   ```

### 5.2 Reto: Deuda Técnica Acumulada

**Problema**:
```
"Implementemos rápido para el demo de inversores"
→ Sin tests unitarios
→ Código hardcodeado
→ Sin documentación

3 meses después:
→ Bugs difíciles de rastrear
→ Nuevas features tardan 3x más
→ Miedo de hacer cambios (código frágil)
```

**Soluciones**:

1. **Regla del Boy Scout**: "Dejar el código mejor de como lo encontraste"
   ```python
   # Cada PR debe incluir:
   # 1. Feature solicitado
   # 2. Refactoring de al menos 1 función legacy
   # 3. Tests para código nuevo Y código refactorizado
   ```

2. **Reservar 20% del Sprint para Tech Debt**
   ```
   Sprint 6 (42 SP total):
   - Features nuevas: 34 SP (80%)
   - Tech debt stories: 8 SP (20%)
     * REMED-TD01: Refactorizar módulo de autenticación
     * REMED-TD02: Agregar tests a API de predicción
   ```

3. **Hacer Deuda Técnica Visible**
   ```
   Dashboard del Equipo:
   
   TECH DEBT TRACKER
   ┌────────────────────────────────────────┐
   │ Total Tech Debt: 45 Story Points      │
   │ Tiempo estimado para pagar: 3 sprints │
   │                                        │
   │ Top 3 Áreas Críticas:                  │
   │ 1. Módulo ML (sin tests): 21 SP       │
   │ 2. Integración EHR (hardcoded): 13 SP │
   │ 3. Dashboard (performance): 8 SP      │
   │                                        │
   │ Tendencia: ⬆ Creciendo (alerta)       │
   └────────────────────────────────────────┘
   ```

### 5.3 Reto: Estimaciones Siempre Incorrectas

**Problema**:
```
Estimado: 5 SP (2-3 días)
Real: 13 SP (toda la semana)

Causas comunes:
- No consideramos integración con sistema legacy
- Subestimamos complejidad del algoritmo ML
- Olvidamos el tiempo de testing
- Surgió bug inesperado en librería de terceros
```

**Soluciones**:

1. **Tracking de Precision de Estimaciones**
   ```
   HISTORIA: REMED-101
   Estimado: 13 SP
   Real: 16 SP
   Variance: +23%
   
   Post-mortem:
   - Subestimamos tiempo de diseño de UI con médicos (2 días extra)
   - Aprendizaje: Agregar buffer para validación médica
   ```

2. **Técnica del Cono de Incertidumbre**
   ```
   Fase del Proyecto          Rango de Error
   ───────────────────────────────────────────
   Concepto inicial           ±100% (4x-0.25x)
   Requisitos aprobados       ±50%  (2x-0.5x)
   Diseño completo            ±25%  (1.5x-0.75x)
   Código escrito             ±10%  (1.1x-0.9x)
   
   → Para historias en backlog lejano:
     Estimar rangos: "Entre 8 y 21 SP"
   → Para próximo sprint:
     Estimar puntualmente: "13 SP"
   ```

3. **Spike Stories para Incertidumbre Técnica**
   ```
   SPIKE: REMED-SP02
   Pregunta: ¿Podemos lograr predicciones <3 seg con 100K pacientes?
   
   Experimentos:
   - Benchmark de PostgreSQL vs Cassandra
   - Probar caching con Redis
   - Optimizar queries SQL
   
   Time-box: 2 días
   Resultado esperado: Documento con recomendación técnica
   
   → Después del spike, estimar REMED-102 con mayor certeza
   ```

### 5.4 Reto: Comunicación en Equipos Distribuidos

**Problema**:
```
Equipo ReMedical distribuido:
- 3 developers en México (GMT-6)
- 2 developers en España (GMT+1)
- 1 QA en Argentina (GMT-3)
- Product Owner en USA (GMT-8)

→ Solo 2 horas de overlap diario
→ Decisiones se retrasan
→ Malentendidos frecuentes en Slack
```

**Soluciones**:

1. **Documentación Asíncrona Exhaustiva**
   ```
   ✅ Cada historia en Jira incluye:
   - Mockups visuales (Figma)
   - Diagramas de flujo
   - Ejemplos de JSON (contratos API)
   - Video de 5 min explicando el feature (Loom)
   
   ❌ No depender de "conversación verbal"
   ```

2. **Daily Standup Asíncrono**
   ```
   Canal Slack: #remedial-standup
   
   Template (cada día antes de 10:00 AM su zona horaria):
   
   👤 Juan Pérez (México)
   ✅ Ayer: Completé frontend de REMED-101
   🎯 Hoy: Integrar con API de ML
   🚫 Bloqueadores: Ninguno
   
   👤 Ana López (España)
   ✅ Ayer: Deploy de modelo en SageMaker
   🎯 Hoy: Optimización de performance (<3s)
   🚫 Bloqueadores: Esperando acceso a instancia p3.2xlarge
   
   → Scrum Master revisa a mediodía (horario común)
   → Resuelve bloqueadores vía Slack/Jira
   ```

3. **"Overlap Hours" Sagrado**
   ```
   Horario común: 2:00 PM - 4:00 PM GMT
   
   Reglas:
   - OBLIGATORIO estar disponible (no meetings externos)
   - Ideal para: pair programming, code reviews urgentes
   - Slack con estado "🟢 Available"
   - Respuestas en <15 minutos
   
   Fuera de overlap hours:
   - Documentar todo en Confluence/Jira
   - Respuestas en <24 horas aceptable
   ```

---

## 6. Mejores Prácticas en Agilismo

### ✅ Mejores Prácticas

#### 1. Definition of Ready (DoR)

**Historia NO entra al sprint sin cumplir**:
```
☐ Narrativa clara (Como/Quiero/Para)
☐ Criterios de aceptación específicos (≥3)
☐ Estimación consensuada por el equipo
☐ Dependencias identificadas y resueltas
☐ Mockups/diseños disponibles (si aplica)
☐ Aprobación de stakeholder clave
☐ Prioridad asignada por Product Owner
```

#### 2. Definition of Done (DoD)

**Historia NO se marca "Done" sin cumplir**:
```
☐ Código en rama main/develop
☐ Tests automatizados (unit + integration)
☐ Code coverage >80%
☐ Code review aprobado (≥2 reviewers)
☐ QA testing manual passed
☐ Performance testing passed (si aplica)
☐ Documentación técnica actualizada
☐ Demo aceptado por Product Owner
☐ Deployment a staging exitoso
☐ No regresiones detectadas
```

#### 3. Sprint Retrospective Efectivo

**Formato: Start-Stop-Continue**
```
Retrospectiva Sprint 5 - ReMedical

🟢 START (Empezar a hacer)
- Pair programming para features complejos de ML
- Revisión de PRs dentro de 24 horas
- Documentar decisiones técnicas en ADRs

🔴 STOP (Dejar de hacer)
- Meetings sin agenda predefinida
- Commits directos a main (forzar PRs)
- Subestimar tiempo de validación médica

🔵 CONTINUE (Seguir haciendo)
- Daily standups de 15 min estrictos ✅
- Demo de features cada viernes ✅
- Celebrar wins del equipo (🍕 pizza party) ✅

📝 ACCION ITEMS con owner:
1. [Juan] Crear template de ADR en Confluence - Due: Nov 12
2. [Ana] Configurar branch protection en GitLab - Due: Nov 8
3. [Carlos] Documentar proceso de validación médica - Due: Nov 15
```

#### 4. Velocity Sostenible

**NO Heroics (No Héroes)**:
```
❌ Malo:
Sprint 5: Team trabaja 60 horas/semana
→ Velocity: 50 SP (récord!)
Sprint 6: Team agotado, 3 enfermos
→ Velocity: 15 SP (colapso)

✅ Bueno:
Sprint 5: Team trabaja 40 horas/semana
→ Velocity: 34 SP (sostenible)
Sprint 6: Mismo ritmo
→ Velocity: 32 SP (consistente)

Mantra: "Agilismo es una maratón, no un sprint"
```

#### 5. Celebrate Wins (Celebrar Logros)

```
Después de cada hito importante:

✅ Sprint completado 100%
   → Team lunch el viernes

✅ MVP lanzado a producción
   → Tarde libre el lunes

✅ Feedback positivo de 10 médicos usuarios
   → Bono de $500 por persona

✅ Paper científico aceptado en conferencia
   → Viaje del equipo a conferencia (pago por empresa)
```

---

## 7. Roles en Equipos Ágiles de ReMedical

### Product Owner (PO)
**Responsabilidades**:
- Definir y priorizar backlog
- Escribir historias de usuario con criterios de aceptación
- Aceptar o rechazar trabajo completado en Sprint Review
- Representar la voz del negocio y usuarios

**En ReMedical**: 
- Lidera entrevistas con médicos para requisitos
- Prioriza features según impacto clínico y regulatorio
- Valida prototipos con stakeholders médicos

### Scrum Master (SM)
**Responsabilidades**:
- Facilitar ceremonias (Planning, Daily, Review, Retro)
- Eliminar impedimentos del equipo
- Coaching en prácticas ágiles
- Proteger al equipo de interrupciones externas

**En ReMedical**:
- Coordina con equipo de compliance para desbloquear aprobaciones FDA
- Facilita colaboración entre devs y científicos médicos
- Escala riesgos técnicos a CTO

### Development Team
**Responsabilidades**:
- Auto-organizarse para completar trabajo del sprint
- Estimar historias de usuario
- Comprometerse con objetivos del sprint
- Implementar, testear y desplegar features

**En ReMedical**:
```
Equipo Multidisciplinario:
├── 2 Frontend Developers (React)
├── 2 Backend Developers (Python/FastAPI)
├── 1 ML Engineer (TensorFlow/PyTorch)
├── 1 Data Engineer (Spark/Airflow)
├── 1 DevOps Engineer (AWS/Kubernetes)
├── 1 QA Engineer (Automation + Manual)
└── 1 Medical Informaticist (liaison con médicos)
```

---

## 8. Métricas Clave en Agilismo

| Métrica | Fórmula | Objetivo ReMedical | Uso |
|---------|---------|-------------------|-----|
| **Velocity** | SP completados/sprint | 32-36 SP/sprint | Planificación de capacidad |
| **Sprint Burndown** | SP restantes vs días | Línea descendente suave | Tracking diario de progreso |
| **Cycle Time** | Tiempo "In Progress" → "Done" | <5 días promedio | Identificar cuellos de botella |
| **Lead Time** | Tiempo "Backlog" → "Done" | <15 días para stories | Velocidad end-to-end |
| **Defect Density** | Bugs/Story Points | <0.1 bugs/SP | Calidad del código |
| **Sprint Completion** | % historias completadas | >90% | Precisión de planificación |
| **Team Happiness** | Encuesta 1-10 | >7.5 promedio | Salud del equipo |

---

## Referencias

- Cohn, M. (2004). User Stories Applied: For Agile Software Development. Addison-Wesley.
- Rubin, K. S. (2012). Essential Scrum: A Practical Guide to the Most Popular Agile Process. Addison-Wesley.
- Patton, J. (2014). User Story Mapping: Discover the Whole Story, Build the Right Product. O'Reilly.
- North, D. (2006). Introducing BDD (Behavior-Driven Development).
- Schwaber, K., & Sutherland, J. (2020). The Scrum Guide. Scrum.org.
