# Ciclo de Vida de Desarrollo de Software en ReMedical

**Versión**: 1.0  
**Fecha**: Noviembre 2025  
**Autor**: Miguel Vengare

---

## Enfoque Híbrido: Ágil + Regulatorio



## Modelos de SDLC Considerados

### Modelo en Cascada (Waterfall)

**Características**:
- Fases secuenciales sin retorno
- Documentación exhaustiva upfront
- Cambios costosos y difíciles

**Ventajas para ReMedical**:
- Trazabilidad completa requerida por FDA
- Documentación detallada para auditorías
- Claridad en entregables de cada fase

**Desventajas**:
- Poca flexibilidad ante cambios de requisitos
- Validación tardía con usuarios
- Alto riesgo de construir producto incorrecto

**Decisión**: No adoptado como modelo único, pero elementos incorporados para cumplimiento regulatorio

### Modelo en V

**Características**:
- Extensión del cascada con énfasis en verificación y validación
- Cada fase de desarrollo tiene fase de testing correspondiente
- Integración de calidad desde el inicio

**Aplicación en ReMedical**:
```
DESARROLLO                           VALIDACIÓN
───────────────────────────────────────────────────

Requisitos de Negocio ─────────────> Acceptance Testing
    |                                      ↑
    |                                      |
    v                                      |
Requisitos de Sistema ──────────────> System Testing
    |                                      ↑
    |                                      |
    v                                      |
Diseño de Arquitectura ─────────────> Integration Testing
    |                                      ↑
    |                                      |
    v                                      |
Diseño Detallado ───────────────────> Unit Testing
    |                                      ↑
    |                                      |
    v                                      |
Implementación ─────────────────────────>
```

**Valor para ReMedical**: Garantiza que cada requisito tiene prueba correspondiente (trazabilidad requerida por FDA)

### Desarrollo Ágil - Scrum

**Características**:
- Iteraciones cortas (sprints de 2 semanas)
- Entrega incremental de valor
- Adaptación continua a cambios

**Implementación en ReMedical**:

**Sprint 0**: Configuración de infraestructura, definición de Definition of Done
**Sprints 1-3**: MVP - Predicción básica de diabetes
**Sprints 4-6**: Integración con EHR, dashboard médico
**Sprints 7-9**: Explicabilidad, reportes, exportación
**Sprints 10-12**: Hardening, certificación FDA, deployment

**Ceremonias Implementadas**:
- Sprint Planning (Lunes, 4 horas)
- Daily Standup (Todos los días, 15 minutos)
- Sprint Review (Viernes, 2 horas con stakeholders médicos)
- Sprint Retrospective (Viernes, 1 hora)
- Backlog Refinement (Miércoles, 1 hora)

**Ventajas para ReMedical**:
- Validación temprana y frecuente con médicos
- Capacidad de respuesta a feedback clínico
- Reducción de riesgo mediante entregas incrementales

### Modelo Híbrido Adoptado

**Decisión Final**: Ágil con Controles de Cascada

**Estructura**:

**Fase 1: Iniciación (Waterfall)**
- Definición de alcance regulatorio
- Identificación de stakeholders críticos
- Análisis de riesgos inicial
- Planificación de certificaciones
- Duración: 4 semanas

**Fase 2: Elaboración (Iterativa)**
- Arquitectura de referencia
- Prototipos de baja fidelidad
- Validación de viabilidad técnica
- Definición de estándares (HL7 FHIR, SNOMED CT)
- Duración: 6 semanas

**Fase 3: Construcción (Scrum)**
- Sprints de 2 semanas
- Entregas incrementales validadas
- Integración continua
- Testing automatizado
- Duración: 24 semanas (12 sprints)

**Fase 4: Transición (Waterfall)**
- Certificación FDA
- Auditoría HIPAA
- Capacitación de usuarios
- Deployment controlado
- Duración: 8 semanas

---

## Fases Detalladas del SDLC en ReMedical

### Fase 1: Recolección y Análisis de Requisitos

**Duración**: 6 semanas

**Actividades**:

**Semana 1-2: Identificación de Stakeholders**
- Mapeo de todos los actores involucrados
- Priorización según influencia e interés
- Planificación de entrevistas

**Resultado**: 
- 23 stakeholders identificados
- 12 seleccionados para entrevistas profundas

**Semana 3-4: Recolección de Datos**
- 12 entrevistas estructuradas con médicos
- 20 horas de observación contextual en consultorios
- 4 workshops multidisciplinarios
- Análisis de 34 papers científicos

**Resultado**:
- 47 requisitos funcionales documentados
- 23 requisitos no funcionales identificados
- 8 restricciones regulatorias mapeadas

**Semana 5-6: Análisis y Validación**
- Detección de conflictos entre requisitos
- Priorización con MoSCoW
- Validación con stakeholders
- Creación de SRS v1.0

**Resultado**:
- SRS aprobado por Product Owner y stakeholders médicos clave
- 4 conflictos resueltos
- Backlog priorizado inicial

**Artefactos Generados**:
- Software Requirements Specification (SRS)
- Matriz de Stakeholders
- Product Backlog v1.0
- Matriz de Trazabilidad inicial

### Fase 2: Diseño del Sistema

**Duración**: 4 semanas

**Diseño de Arquitectura (Semana 1-2)**:

**Decisiones Arquitectónicas**:
- Arquitectura de microservicios (escalabilidad, mantenibilidad)
- Backend: Python FastAPI + XGBoost (predicción ML)
- Frontend: React + TypeScript (UI responsiva)
- Base de datos: PostgreSQL (datos estructurados) + MongoDB (logs, auditoría)
- Infraestructura: AWS (EC2, RDS, S3, CloudWatch)
- Integración: HL7 FHIR para interoperabilidad con EHR

**Diagrama de Arquitectura**:
```
┌─────────────┐
│   Browser   │
└──────┬──────┘
       │ HTTPS/TLS 1.3
       ↓
┌─────────────────────────────────┐
│  React Frontend (TypeScript)    │
│  - Dashboard Médico             │
│  - Visualización de Predicción  │
└──────┬──────────────────────────┘
       │ REST API
       ↓
┌─────────────────────────────────┐
│  API Gateway (AWS)              │
│  - Autenticación OAuth 2.0      │
│  - Rate Limiting                │
└──────┬──────────────────────────┘
       │
       ├───────────────────────┬────────────────────┐
       ↓                       ↓                    ↓
┌──────────────┐    ┌──────────────────┐   ┌─────────────┐
│ Prediction   │    │ Integration      │   │ Audit       │
│ Service      │    │ Service          │   │ Service     │
│ (FastAPI)    │    │ (HL7 FHIR)       │   │ (Logging)   │
└──────┬───────┘    └────────┬─────────┘   └──────┬──────┘
       │                     │                     │
       ↓                     ↓                     ↓
┌──────────────┐    ┌──────────────┐      ┌─────────────┐
│ PostgreSQL   │    │ EHR Systems  │      │ MongoDB     │
│ (Patient DB) │    │ (External)   │      │ (Audit Log) │
└──────────────┘    └──────────────┘      └─────────────┘
```

**Diseño Detallado (Semana 3-4)**:

**Modelos de Datos**:
```python
# Modelo de Paciente
Patient:
  id: UUID
  mrn: String (Medical Record Number)
  demographics: Demographics
  clinical_data: ClinicalData
  predictions: List[Prediction]
  created_at: Timestamp
  updated_at: Timestamp

# Modelo de Predicción
Prediction:
  id: UUID
  patient_id: UUID
  risk_score: Float (0-100)
  risk_category: Enum (LOW, MEDIUM, HIGH)
  contributing_factors: Dict[String, Float]
  model_version: String
  confidence_interval: Tuple[Float, Float]
  created_at: Timestamp
  created_by: UUID (médico)
```

**Diseño de Interfaces**:
- Wireframes de baja fidelidad validados
- Prototipos de alta fidelidad en Figma
- 23 pantallas diseñadas
- 8 flujos de usuario documentados

**Artefactos Generados**:
- Documento de Arquitectura de Software (SAD)
- Diagramas UML (clases, secuencia, componentes)
- Especificaciones de API (OpenAPI/Swagger)
- Prototipos interactivos

### Fase 3: Implementación

**Duración**: 24 semanas (12 sprints de 2 semanas)

**Estructura de Sprint**:

**Sprint Planning (Lunes)**:
- Selección de historias del backlog (velocity: 34 story points promedio)
- Descomposición en tareas técnicas
- Estimación con Planning Poker
- Definición de Sprint Goal

**Desarrollo (Martes-Jueves)**:
- Pair programming para código crítico (algoritmo de predicción)
- Code reviews obligatorios (mínimo 2 aprobaciones)
- Test-Driven Development (TDD) para lógica de negocio
- Integración continua con GitHub Actions

**Testing (Viernes mañana)**:
- Unit tests (coverage >80%)
- Integration tests
- Smoke tests en staging

**Sprint Review (Viernes tarde)**:
- Demo a stakeholders médicos
- Recolección de feedback
- Actualización de backlog

**Ejemplos de Sprint Goals**:
- Sprint 1: "Usuario puede autenticarse y ver lista de pacientes"
- Sprint 5: "Sistema calcula predicción de diabetes con modelo baseline"
- Sprint 9: "Dashboard muestra explicabilidad de predicción con SHAP values"

**Prácticas de Calidad**:
- Linting automático (flake8, ESLint)
- Type checking (mypy para Python, TypeScript para frontend)
- Security scanning (Snyk, OWASP Dependency Check)
- Performance profiling (cada 3 sprints)

**Gestión de Ramas**:
```
main (producción)
  ↑
  └── develop (integración)
       ↑
       ├── feature/REMED-123-risk-calculation
       ├── feature/REMED-124-dashboard-ui
       └── bugfix/REMED-125-fix-auth-token
```

**Artefactos Generados por Sprint**:
- Código fuente versionado
- Tests automatizados
- Incremento de producto potencialmente entregable
- Actualización de documentación técnica

### Fase 4: Pruebas y Validación

**Integrada en cada Sprint + Fase Dedicada Final (4 semanas)**

**Niveles de Testing**:

**Unit Testing** (continuo):
- Framework: pytest (Python), Jest (TypeScript)
- Coverage objetivo: 80%
- Ejecutados en cada commit (CI/CD)
- Resultado: 1,243 unit tests, 84% coverage

**Integration Testing** (cada sprint):
- Testing de APIs
- Testing de integración con base de datos
- Testing de integración con EHR simulado
- Resultado: 187 integration tests

**System Testing** (cada 3 sprints):
- End-to-end testing con Cypress
- Testing de flujos completos de usuario
- Testing de no-funcionales (performance, seguridad)
- Resultado: 45 E2E tests

**User Acceptance Testing** (semanas 27-28):
- 8 médicos endocrinólogos
- 30 días de uso en ambiente de staging
- 324 predicciones realizadas en escenarios reales
- Resultado: 89% satisfacción, 3 bugs menores identificados

**Regulatory Testing** (semanas 29-30):
- Validación FDA: evidencia de trazabilidad completa
- Auditoría HIPAA: penetration testing, revisión de controles
- Resultado: Aprobado en primer intento

**Artefactos de Testing**:
- Plan de Pruebas Maestro
- Casos de prueba documentados (342 casos)
- Reportes de ejecución automatizados
- Matriz de Trazabilidad actualizada (127 vínculos)

### Fase 5: Despliegue

**Duración**: 3 semanas

**Estrategia de Deployment**:

**Semana 1: Preparación**
- Migración de datos de desarrollo a producción
- Configuración de infraestructura AWS producción
- Setup de monitoreo (CloudWatch, Datadog)
- Preparación de rollback plan

**Semana 2: Despliegue Piloto**
- Deployment a 2 hospitales (50 usuarios)
- Monitoreo intensivo 24/7
- Soporte técnico on-site
- Recolección de métricas en tiempo real

**Métricas Monitoreadas**:
- Tiempo de respuesta API (P50, P95, P99)
- Tasa de errores (objetivo: <0.1%)
- Uso de recursos (CPU, memoria, DB connections)
- Satisfacción de usuarios (Net Promoter Score)

**Semana 3: Rollout Completo**
- Expansión a 8 hospitales adicionales (300 usuarios)
- Capacitación de usuarios finales (webinars, documentación)
- Handoff a equipo de soporte

**Artefactos de Despliegue**:
- Runbook de operaciones
- Plan de rollback
- Guías de usuario
- Documentación de API para integradores

### Fase 6: Mantenimiento y Evolución

**Modelo de Soporte**:

**Soporte L1** (Help Desk):
- Horario: 24/7
- Tiempo de respuesta: <1 hora
- Resolución de issues comunes

**Soporte L2** (Equipo Técnico):
- Horario: 8 AM - 8 PM
- Bugs, configuración, troubleshooting

**Soporte L3** (Ingeniería)**:
- On-call para incidentes críticos
- Desarrollo de fixes y patches

**Ciclo de Mantenimiento**:
- Releases menores: cada 2 semanas (bugfixes, mejoras menores)
- Releases mayores: cada 3 meses (nuevas funcionalidades)
- Parches de seguridad: según necesidad (SLA 48 horas para críticos)

**Monitoreo Continuo**:
- Uptime: 99.9% (objetivo)
- Performance: P95 <3 segundos
- Accuracy del modelo: re-evaluación trimestral
- Feedback de usuarios: NPS mensual

---

## Adaptaciones para Cumplimiento Regulatorio

### FDA Class II Medical Device Software

**Requisitos Específicos**:

**Design Controls** (21 CFR 820.30):
- Documentación de requisitos de diseño
- Revisiones formales en cada fase
- Verificación y validación documentadas
- Design History File (DHF) completo

**Implementación en ReMedical**:
- Matriz de trazabilidad completa (requisitos → diseño → código → tests)
- Revisiones formales con actas firmadas
- 342 casos de prueba documentados con resultados
- DHF de 850 páginas mantenido en Confluence

**Risk Management** (ISO 14971):
- Análisis de riesgos de cada requisito
- FMEA (Failure Mode and Effects Analysis)
- Mitigaciones documentadas y verificadas

**Ejemplo de Análisis de Riesgo**:
```
Riesgo: Predicción incorrecta de bajo riesgo para paciente de alto riesgo
Probabilidad: Baja (modelo con recall >85%)
Severidad: Alta (paciente no recibe intervención necesaria)
Mitigación: 
  - Disclaimer para médicos: predicción es apoyo, no diagnóstico
  - Umbral conservador de clasificación
  - Revisión periódica de casos borderline
  - Alert para médico si factores conflictivos
Estado: Riesgo aceptable con mitigaciones
```

### HIPAA Compliance

**Requisitos de Seguridad**:
- Encriptación de datos en tránsito y reposo
- Control de acceso basado en roles (RBAC)
- Auditoría de acceso a PHI
- Business Associate Agreements con proveedores

**Implementación**:
- TLS 1.3 para comunicación
- AES-256 para datos en reposo
- OAuth 2.0 + SAML para autenticación
- Logs inmutables de auditoría en MongoDB

---

## Métricas del Ciclo de Vida

**Duración Total**: 41 semanas (9.5 meses)

**Distribución de Esfuerzo**:
- Requisitos: 10% (340 horas-persona)
- Diseño: 12% (408 horas-persona)
- Implementación: 60% (2,040 horas-persona)
- Testing: 12% (408 horas-persona)
- Despliegue: 6% (204 horas-persona)

**Velocidad de Desarrollo**:
- Velocity promedio: 34 story points/sprint
- 127 historias de usuario completadas
- 3 historias movidas a backlog futuro

**Calidad**:
- Bugs en producción (primer mes): 7 (todos severidad baja)
- Defects per KLOC: 0.8 (industry avg: 1-5)
- Customer satisfaction: 89% (UAT)

**Retorno de Inversión**:
- Costo total desarrollo: $850,000
- Tiempo ahorrado por médico: 8 minutos/día
- ROI proyectado a 2 años: 240%

---

## Lecciones Aprendidas

**Lo que Funcionó**:
1. Modelo híbrido permitió flexibilidad sin sacrificar cumplimiento
2. Validación frecuente con stakeholders evitó sorpresas
3. Inversión upfront en arquitectura previno deuda técnica

**Desafíos Enfrentados**:
1. Integración con EHR legados más compleja de lo estimado
2. Requisitos regulatorios emergentes durante desarrollo
3. Rotación de personal médico en hospitales piloto

**Recomendaciones para Futuros Proyectos**:
1. Buffer de 20% en estimaciones para proyectos regulados
2. Asesor regulatorio desde día 1
3. Documentación continua, no al final

---

## Referencias

- FDA Guidance: Software as a Medical Device (SaMD)
- ISO/IEC 12207: Software Life Cycle Processes
- Scrum Guide 2020
- ISO 14971: Medical Devices - Risk Management
- 21 CFR Part 820: FDA Quality System Regulation

---

**Historial de Versiones**:
- v1.0 (2025-11-05): Versión inicial completa

**Próxima Revisión**: 2025-12-05
