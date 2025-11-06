# Retos y Mejores Prácticas en Agilismo

**Versión**: 1.0  
**Fecha**: Noviembre 2025

---

## Retos Anticipados

### 1. Compliance Regulatorio vs. Agilidad

**Desafío**: FDA requiere documentación exhaustiva, waterfall-friendly.

**Estrategia**:
- Documentación incremental durante sprints
- Automated testing como evidencia
- Confluence para documentación viva
- Design History File actualizado continuamente

---

### 2. Disponibilidad de Stakeholders Médicos

**Desafío**: Médicos con agenda saturada, poca disponibilidad para demos.

**Estrategia**:
- Sprint Reviews grabadas (async)
- Demos de 30 min máximo
- Prototipos interactivos para validación independiente
- Compensación económica por tiempo

---

### 3. Requisitos Ambiguos Inicialmente

**Desafío**: Stakeholders pueden no saber qué quieren exactamente.

**Estrategia**:
- Prototipos de baja fidelidad tempranos
- User Story Mapping para visualizar flujo
- Iteraciones cortas con feedback rápido
- "Fail fast" philosophy

---

### 4. Integración con EHR Legados

**Desafío**: APIs de EHR no siempre bien documentadas.

**Estrategia**:
- Spike stories para investigación técnica
- Mockups de EHR para desarrollo paralelo
- Colaboración directa con vendor de EHR
- Capa de abstracción (Adapter pattern)

---

### 5. Estimación Imprecisa Inicial

**Desafío**: Primeros sprints con estimaciones potencialmente erróneas.

**Estrategia**:
- Refinamiento continuo de técnica de estimación
- Historical data de sprints previos
- Descomposición de historias grandes
- Buffer de 20% para imprevistos

---

## Mejores Prácticas a Aplicar

### 1. Product Owner Dedicado

PO tiempo completo, sin otras responsabilidades.

---

### 2. Cross-Functional Team

Equipo con todas las skills necesarias (frontend, backend, ML, QA, DevOps).

---

### 3. Working Software sobre Documentación

Balance: 80% tiempo en código, 20% en documentación (suficiente para FDA).

---

### 4. Retrospectivas Accionables

Cada retrospectiva genera 1-3 acciones concretas con responsable y deadline.

---

### 5. Technical Debt Management

20% de cada sprint dedicado a technical debt y refactoring.

**Métrica objetivo**: Technical Debt Ratio <5% (SonarQube).

---

### 6. Automated Testing

TDD, CI/CD con tests automáticos, no merge sin pasar tests.

**Cobertura objetivo**:
- Unit tests: >80%
- Integration tests: >70%
- E2E tests: Flujos críticos

---

### 7. Priorización MoSCoW

Must/Should/Could/Won't Have para claridad de prioridades.

**Distribución objetivo**:
- Must Have: 40% (MVP)
- Should Have: 35%
- Could Have: 20%
- Won't Have: 5%

---

### 8. Stakeholder Engagement Continuo

Sprint Reviews con demos reales, no slides.

**Formato**:
- 10 min: Sprint Goal
- 40 min: Demo funcionalidades
- 40 min: Feedback
- 30 min: Próximos pasos

---

## Anti-Patterns a Evitar

### 1. Scrum-But
"Hacemos Scrum, pero..." (sin retrospectivas, sin demos, etc.)

**Prevención**: Compromiso con framework completo, coach externo inicial.

---

### 2. Sprint Zero Infinito
Sprints de "setup" sin entregar valor.

**Prevención**: Sprint 0 máximo 2 semanas.

---

### 3. Historias Técnicas sin Valor de Negocio
"Como desarrollador, quiero refactorizar..."

**Prevención**: Historias desde perspectiva de usuario.

---

### 4. Product Owner Ausente
PO no disponible, decisiones bloqueadas.

**Prevención**: PO tiempo completo, backup designado.

---

### 5. Sprints sin Incremento Entregable
"Casi terminado pero no deployable".

**Prevención**: Definition of Done estricto.

---

## Métricas Objetivo

| Métrica | Target |
|---------|--------|
| Velocity estabilizada (sprint 6+) | ±15% |
| Asistencia Sprint Review | >80% |
| Historias completadas/sprint | >90% |
| Time-to-market (MVP) | 6 meses |
| Satisfacción equipo (NPS) | >7/10 |
| Satisfacción stakeholders | >80% |
