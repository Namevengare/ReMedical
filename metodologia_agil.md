# Metodología Ágil - ReMedical

---

## Framework: Scrum

**Sprints**: 2 semanas  
**Equipo**: 8 personas (1 PO, 1 SM, 6 devs)  
**Velocity objetivo**: Estabilizar tras 6 sprints

---

## Ceremonias

### Sprint Planning (Lunes, 4h)
- Selección de historias del backlog
- Descomposición en tareas
- Estimación con Planning Poker
- Definición de Sprint Goal

### Daily Standup (Diario, 15min)
- ¿Qué hice ayer?
- ¿Qué haré hoy?
- ¿Qué impedimentos tengo?

### Sprint Review (Viernes, 2h)
- Demo a stakeholders médicos
- Feedback y validación
- Actualización de backlog

### Sprint Retrospective (Viernes, 1h)
- ¿Qué funcionó bien?
- ¿Qué mejorar?
- Acciones concretas para siguiente sprint

### Backlog Refinement (Miércoles, 1h)
- Clarificación de historias futuras
- Estimación preliminar
- Identificación de dependencias

---

## Definition of Ready

Una historia está lista para sprint cuando:
- Tiene criterios de aceptación claros
- Está estimada por el equipo
- Sin dependencias bloqueantes
- Mockups disponibles (si aplica)
- Product Owner la priorizó

## Definition of Done

Una historia está completa cuando:
- Código implementado según criterios
- Tests con coverage >80%
- Code review aprobado (2+ reviewers)
- Desplegado en staging
- QA aprobó
- Documentación actualizada
- Product Owner aceptó

---

## Prácticas de Desarrollo

### Test-Driven Development (TDD)
- Red: Escribir test que falla
- Green: Implementar código mínimo
- Refactor: Mejorar diseño

### Pair Programming
- Para código crítico (algoritmo predicción)
- Rotación de pares cada día
- Junior + Senior para mentoring

### Code Reviews
- Mínimo 2 aprobaciones
- Checklist: lógica, tests, seguridad, performance
- Tiempo máximo de review: 24 horas

### Continuous Integration
- GitHub Actions
- Tests automáticos en cada commit
- Build debe pasar antes de merge

---

## Métricas a Monitorear

**Velocity**: Story points completados por sprint  
**Burndown**: Trabajo restante vs. tiempo  
**Cycle Time**: Tiempo desde inicio hasta done  
**Lead Time**: Tiempo desde backlog hasta producción  
**Defect Density**: Bugs por 1000 líneas de código  
**Code Coverage**: Porcentaje de código con tests

**Objetivos**:
- Velocity estabilizada (sprint 6+): ±15%
- Historias completadas por sprint: >90%
- Test coverage: >80%
- Satisfacción UAT: >80%

---

## Adaptaciones para Regulatorio

**FDA Compliance**:
- Documentación formal de cada release
- Trazabilidad completa (requisitos → tests)
- Revisiones formales con actas firmadas
- Design History File (DHF) actualizado

**HIPAA Compliance**:
- Security reviews en cada sprint
- Penetration testing trimestral
- Logs de auditoría inmutables
- Encryption obligatorio

---


