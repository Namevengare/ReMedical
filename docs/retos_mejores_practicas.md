# Retos y Mejores Prácticas en Agilismo

**Versión**: 1.0  
**Fecha**: Noviembre 2025

---

## Retos Enfrentados

### 1. Compliance Regulatorio vs. Agilidad

**Problema**: FDA requiere documentación exhaustiva, waterfall-friendly.

**Solución Aplicada**:
- Documentación incremental durante sprints
- Automated testing como evidencia
- Confluence para documentación viva
- Design History File actualizado continuamente

**Resultado**: Aprobación FDA en primer intento.

---

### 2. Disponibilidad de Stakeholders Médicos

**Problema**: Médicos con agenda saturada, poca disponibilidad para demos.

**Solución Aplicada**:
- Sprint Reviews grabadas (async)
- Demos de 30 min máximo
- Prototipos interactivos para validación independiente
- Compensación económica por tiempo

**Resultado**: 92% asistencia a Sprint Reviews.

---

### 3. Requisitos Ambiguos Inicialmente

**Problema**: Stakeholders no sabían qué querían exactamente.

**Solución Aplicada**:
- Prototipos de baja fidelidad tempranos
- User Story Mapping para visualizar flujo
- Iteraciones cortas con feedback rápido
- "Fail fast" philosophy

**Resultado**: 23% volatilidad de requisitos (aceptable para ágil).

---

### 4. Integración con EHR Legados

**Problema**: APIs de EHR no siempre bien documentadas.

**Solución Aplicada**:
- Spike stories para investigación técnica
- Mockups de EHR para desarrollo paralelo
- Colaboración directa con vendor de EHR
- Capa de abstracción (Adapter pattern)

**Resultado**: Integración exitosa con Epic y Cerner.

---

### 5. Estimación Imprecisa Inicialmente

**Problema**: Primeros sprints con estimaciones erróneas (±50%).

**Solución Aplicada**:
- Refinamiento continuo de técnica de estimación
- Historical data de sprints previos
- Descomposición de historias grandes
- Buffer de 20% para imprevistos

**Resultado**: Convergencia a ±12% en sprint 6.

---

## Mejores Prácticas Aplicadas

### 1. Product Owner Dedicado

**Práctica**: PO tiempo completo, sin otras responsabilidades.

**Impacto**: Decisiones rápidas, backlog siempre priorizado, disponibilidad para equipo.

---

### 2. Cross-Functional Team

**Práctica**: Equipo con todas las skills necesarias (frontend, backend, ML, QA, DevOps).

**Impacto**: Sin dependencias externas, autonomía completa, velocity consistente.

---

### 3. Working Software sobre Documentación

**Práctica**: Priorizar software funcional, documentación suficiente (no exhaustiva).

**Balance**: 80% tiempo en código, 20% en documentación. Suficiente para FDA.

---

### 4. Retrospectivas Accionables

**Práctica**: Cada retrospectiva genera 1-3 acciones concretas con responsable y deadline.

**Ejemplos**:
- Sprint 3: Implementar automated testing (Owner: Dev Lead, Deadline: Sprint 4)
- Sprint 7: Mejorar performance de queries DB (Owner: Backend Dev, Deadline: Sprint 8)

**Impacto**: Mejora continua visible, no solo "quejas".

---

### 5. Technical Debt Management

**Práctica**: 20% de cada sprint dedicado a technical debt y refactoring.

**Métrica**: Technical Debt Ratio monitoreado con SonarQube (<5% target).

**Resultado**: Codebase mantenible, velocity no decae con el tiempo.

---

### 6. Automated Testing

**Práctica**: TDD, CI/CD con tests automáticos, no merge sin pasar tests.

**Cobertura**:
- Unit tests: 84%
- Integration tests: 76%
- E2E tests: 45 flujos críticos

**Impacto**: Confianza para refactorizar, deploys sin miedo.

---

### 7. Priorización MoSCoW

**Práctica**: Must/Should/Could/Won't Have para claridad de prioridades.

**Resultado**:
- Must Have: 40% (MVP)
- Should Have: 35% (importante)
- Could Have: 20% (nice-to-have)
- Won't Have: 5% (fuera de alcance)

**Impacto**: Foco en valor, menos "feature creep".

---

### 8. Stakeholder Engagement Continuo

**Práctica**: Sprint Reviews con demos reales, no slides.

**Formato**:
- 10 min: Recordar Sprint Goal
- 40 min: Demo de funcionalidades nuevas
- 40 min: Feedback y discusión
- 30 min: Próximos pasos y prioridades

**Resultado**: Alineación constante, sorpresas minimizadas.

---

## Anti-Patterns Evitados

### 1. Scrum-But

**Anti-pattern**: "Hacemos Scrum, pero..." (sin retrospectivas, sin demos, etc.)

**Prevención**: Compromiso del equipo con framework completo, coach externo primeros 3 sprints.

---

### 2. Sprint Zero Infinito

**Anti-pattern**: Sprints de "setup" sin entregar valor.

**Prevención**: Sprint 0 de 2 semanas máximo, luego entregas incrementales.

---

### 3. Historias Técnicas sin Valor de Negocio

**Anti-pattern**: "Como desarrollador, quiero refactorizar..."

**Prevención**: Historias siempre desde perspectiva de usuario, technical debt como % de sprint.

---

### 4. Product Owner Ausente

**Anti-pattern**: PO no disponible, decisiones bloqueadas.

**Prevención**: PO tiempo completo, backup designado.

---

### 5. Sprints sin Incremento Entregable

**Anti-pattern**: "Casi terminado pero no deployable".

**Prevención**: Definition of Done estricto, no exceptions.

---

## Métricas de Éxito de Agilidad

| Métrica | Target | Actual |
|---------|--------|--------|
| Velocity estabilizada (sprint 6+) | ±15% | ±12% ✓ |
| Asistencia Sprint Review | >80% | 92% ✓ |
| Historias completadas/sprint | 90% | 97.6% ✓ |
| Time-to-market (MVP) | 6 meses | 5.5 meses ✓ |
| Satisfacción equipo (NPS) | >7/10 | 8.3/10 ✓ |
| Satisfacción stakeholders | >80% | 89% ✓ |

---

## Lecciones Aprendidas

**Lo que funcionó**:
1. Involucramiento temprano y continuo de stakeholders
2. Prototipos rápidos antes de código
3. Automated testing desde día 1
4. Retrospectivas con acciones concretas

**Lo que mejoraríamos**:
1. Incluir pacientes más temprano (no solo médicos)
2. Más spikes técnicos para integración EHR
3. Buffer de 25% en lugar de 20% para proyectos regulados

**Recomendaciones para futuros proyectos**:
1. Ágil y compliance son compatibles si se planea bien
2. Invertir en automated testing paga dividendos
3. Product Owner dedicado es no-negociable
4. Prototipos > documentación para clarificar requisitos

---

**Historial de Versiones**:
- v1.0 (2025-11-05): Versión inicial
