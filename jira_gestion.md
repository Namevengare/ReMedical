# Gestión con Jira - ReMedical

**Versión**: 1.0  
**Fecha**: Noviembre 2025

---

## Configuración del Proyecto

**Tipo de proyecto**: Scrum  
**Board**: ReMedical Sprint Board  
**Workflow**: To Do → In Progress → Code Review → QA → Done

---

## Estructura de Issues

### Epic
Funcionalidad grande que abarca múltiples sprints.

**Ejemplo**:
```
Epic: Sistema de Predicción de Diabetes
ID: REMED-EP-001
Descripción: Implementar modelo ML para predicción de riesgo
Story Points: 89
Status: Done
```

### Story
Historia de usuario implementable en 1 sprint.

**Template**:
```
Title: Como [rol] quiero [funcionalidad] para [beneficio]
Epic: [Link a Epic]
Priority: High/Medium/Low
Story Points: [Fibonacci: 1,2,3,5,8,13]
Sprint: Sprint X
Assignee: [Developer]
Labels: frontend, backend, ml, security, etc.

Criterios de Aceptación:
- [ ] Criterio 1
- [ ] Criterio 2
- [ ] Criterio 3

Notas Técnicas:
[Información técnica relevante]

Dependencias:
- Bloqueada por: REMED-123
- Bloquea a: REMED-456
```

### Task
Tarea técnica derivada de una story.

**Ejemplo**:
```
Title: Implementar endpoint POST /predictions
Parent: REMED-US-010 (Cálculo de Predicción)
Estimate: 4 horas
Assignee: Developer A
```

### Bug
Defecto encontrado en testing o producción.

**Template**:
```
Title: [Componente] Descripción concisa del bug
Severity: Critical/High/Medium/Low
Priority: Blocker/High/Medium/Low
Environment: Production/Staging/Development
Steps to Reproduce:
1. 
2. 
3. 
Expected Result:
Actual Result:
Screenshots/Logs: [Adjuntar]
Assignee: [Developer]
Sprint: [Si es blocker]
```

---

## Workflow Estados

### To Do
- Historia en backlog, lista para sprint
- Criterios de aceptación definidos
- Estimada por equipo

### In Progress
- Developer trabajando activamente
- Branch creado en Git
- Daily updates en comentarios

### Code Review
- Pull Request creado
- Mínimo 2 reviewers asignados
- Automated tests pasando

### QA
- QA ejecutando test cases
- Validando criterios de aceptación
- Reportando bugs si los hay

### Done
- Todos criterios cumplidos
- Código en master/main
- Desplegado en staging
- Product Owner aprobó

---

## Campos Personalizados

**Story Points**: Estimación Fibonacci (1,2,3,5,8,13,21)  
**Sprint**: Sprint actual asignado  
**Epic Link**: Epic padre  
**Labels**: frontend, backend, ml, security, infrastructure, documentation  
**Regulatory Impact**: Yes/No (afecta compliance FDA/HIPAA)  
**Test Coverage**: % coverage alcanzado  

---

## Gestión de Sprints

### Creación de Sprint
1. Click en "Create Sprint"
2. Nombrar: "Sprint X - [Fecha Inicio] to [Fecha Fin]"
3. Duration: 2 semanas
4. Goal: Definir objetivo claro del sprint

### Planning
1. Drag historias de backlog a sprint
2. Verificar Definition of Ready
3. Total story points según velocity proyectada
4. Assign a developers

### Durante Sprint
- Daily: Actualizar status de issues
- Move cards a través del board
- Comentar blockers o updates significativos

### Sprint Closure
1. Review: Marcar historias como Done
2. Incomplete: Mover a siguiente sprint o backlog
3. Complete Sprint en Jira
4. Generar reportes

---

## Reportes Utilizados

### Burndown Chart
Trabajo restante (story points) vs. tiempo.

**Indicadores**:
- Línea por encima de ideal: Sprint en riesgo
- Línea por debajo: Buen progreso
- Flat lines: Trabajo bloqueado

### Velocity Chart
Story points completados por sprint.

**Uso**: Planificación de futuros sprints, detectar tendencias.

### Cumulative Flow Diagram
Distribución de issues por estado a lo largo del tiempo.

**Uso**: Identificar bottlenecks (ej: muchas en Code Review).

### Sprint Report
Resumen de sprint: completado vs. no completado.

**Métricas objetivo**:
- Ratio: Completed/Commitment >90%

---

## Backlog Refinement en Jira

**Frecuencia**: Semanal (miércoles)  
**Participants**: PO + Tech Lead + 2-3 developers

**Actividades**:
1. Clarificar historias top del backlog
2. Descomponer historias grandes (>13 SP)
3. Estimar con Planning Poker
4. Ordenar por prioridad (drag & drop)
5. Identificar dependencias (link issues)

---

## Priorización

**Orden del Backlog**:
1. Bugs críticos (Blocker/High severity)
2. Must Have stories (MoSCoW)
3. Should Have stories
4. Technical Debt (20% capacity)
5. Could Have stories

**Filtros Rápidos**:
- `priority = High AND status != Done`
- `labels = security AND sprint is EMPTY`
- `"Story Points" > 13` (historias a descomponer)

---

## Integraciones

### GitHub
- Commits: `REMED-123: Implement prediction endpoint`
- Pull Requests automáticamente linkean a Jira issues
- Status se actualiza al merge

### Confluence
- Specs técnicas linkean a epics/stories
- Documentación de arquitectura referenciada

### Slack
- Notificaciones de status changes
- Canal #remedial-dev para alerts

---

## Métricas a Monitorear

| Métrica | Objetivo |
|---------|----------|
| Velocity | Estabilizar tras 6 sprints |
| Completion Rate | >90% |
| Bugs Creados | Tendencia decreciente |
| Avg Cycle Time | <3 días |

---

## Mejores Prácticas

1. **Historias pequeñas**: Ninguna >13 SP
2. **Criterios claros**: 100% historias con acceptance criteria
3. **Updates diarios**: Comentarios con progreso
4. **Links exhaustivos**: Dependencias siempre linkeadas
5. **Labels consistentes**: Taxonomía definida
6. **Bug triage**: <24 horas

---

## Ejemplo: Template Historia

```
REMED-US-010: Cálculo de Predicción de Riesgo

Epic Link: REMED-EP-001 (Sistema de Predicción)
Priority: High (Must Have)
Story Points: 13
Labels: ml, backend, core-feature
Regulatory Impact: Yes (FDA Class II device)

Descripción:
Como médico endocrinólogo
Quiero calcular el riesgo de diabetes de un paciente con un click
Para identificar pacientes de alto riesgo que requieren intervención

Criterios de Aceptación:
- [ ] Botón "Calcular Riesgo" visible en perfil de paciente
- [ ] Sistema valida datos mínimos (edad, IMC, glucosa/HbA1c)
- [ ] Predicción completa en <3 segundos (P95)
- [ ] Resultado muestra: % riesgo, categoría, confianza
- [ ] Código de colores: Verde (0-30%), Amarillo (31-60%), Rojo (61-100%)
- [ ] Resultado guardado en BD con timestamp y user_id
- [ ] Log de auditoría registra predicción

Notas Técnicas:
- Modelo: XGBoost pre-entrenado
- API: POST /api/v1/predictions
- Input: patient_id + current timestamp
- Output: {risk_score, risk_category, confidence, factors}

Dependencias:
- Bloqueada por: REMED-US-002 (Perfil de Paciente)
- Bloquea a: REMED-US-011 (Explicabilidad)

Subtasks:
- [ ] Implementar endpoint API (4h)
- [ ] Integrar modelo ML (6h)
- [ ] UI botón y loading state (3h)
- [ ] Tests unitarios backend (4h)
- [ ] Tests E2E (5h)
- [ ] Documentación API (2h)

Definition of Done:
- [ ] Código implementado según criterios
- [ ] Tests coverage >80%
- [ ] Code review aprobado
- [ ] Desplegado en staging
- [ ] QA ejecutó test cases
- [ ] Performance test: P95 <3 seg
- [ ] Documentación actualizada
- [ ] Product Owner aprobó
```
