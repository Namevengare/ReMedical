# Validación y Verificación (V&V) - ReMedical

## Conceptos

**Verificación**: ¿Construimos el producto correctamente?
- Conformidad con especificaciones
- Métodos: Revisiones, inspecciones, testing

**Validación**: ¿Construimos el producto correcto?
- Satisfacción de necesidades del usuario
- Métodos: Pruebas de usuario, demos, prototipos

| Aspecto | Verificación | Validación |
|---------|--------------|------------|
| Momento | Durante desarrollo | Al final |
| Evaluadores | Equipo técnico, QA | Usuarios, stakeholders |
| Objetivo | Conformidad specs | Satisfacción necesidades |

## Ciclo de Verificación y Validación

```
Requisitos de Negocio -----------> Acceptance Testing
        |                                  ^
        v                                  |
Requisitos de Sistema -----------> System Testing
        |                                  ^
        v                                  |
Diseño Arquitectura -------------> Integration Testing
        |                                  ^
        v                                  |
Diseño Detallado ----------------> Unit Testing
        |                                  ^
        v                                  |
    IMPLEMENTACIÓN -------------------------
```

---

## Técnicas de Verificación

### Revisiones de Requisitos

**Checklist**:

**Completo**:
- Especifica entradas necesarias
- Define salidas esperadas
- Incluye manejo de excepciones

**Correcto**:
- Técnicamente factible
- Libre de contradicciones
- Stakeholders aprueban

**Consistente**:
- Consistente con otros requisitos
- Terminología estándar

**No Ambiguo**:
- Una sola interpretación
- Cuantificadores claros

**Verificable**:
- Testeable objetivamente
- Criterios de aceptación claros

**Trazable**:
- Vinculado a necesidad de negocio
- ID único y versionado

**Priorizado**:
- Prioridad asignada (MoSCoW)
- Justificación clara

**Regulatorio**:
- Cumple FDA/HIPAA
- Aprobación ética si requiere

### Inspección Formal (Fagan)

**Proceso**:

1. **Planificación**: Moderador, autor, revisores, material
2. **Visión General**: Presentación contexto
3. **Preparación Individual**: Cada revisor analiza
4. **Reunión de Inspección**: Revisión línea por línea, registro defectos
5. **Corrección**: Autor corrige
6. **Seguimiento**: Verificación correcciones

**Roles**:
- Moderador
- Autor
- Revisores (Dev, Médico, QA, Legal)

### Análisis Automatizado (NLP)

**Herramientas**: IBM DOORS, Jama Connect

**Detección automática**:
- Términos vagos ("rápidamente", "bonitos")
- Términos ambiguos ("todos los pacientes")
- Falta de cuantificación
- Lenguaje pasivo

**Mejora sugerida**: Convertir requisitos vagos en específicos con métricas cuantificables

### Requisitos No Funcionales (ISO 25010)

**Categorías**:

**Performance**:
- Método: Performance testing (JMeter)
- Criterios: P50, P95, P99

**Seguridad**:
- Método: Auditoría + Penetration testing
- Checklist: Encriptación tránsito/reposo, gestión claves, auditoría

**Usabilidad**:
- Método: Usability testing con usuarios reales
- Criterios: Tiempo completar tarea, tasa éxito, feedback

---

## Técnicas de Validación

### Prototipado Rápido

**Fases**:

1. **Prototipo Baja Fidelidad**: Wireframes papel
   - Validación con stakeholders (30 min)
   - Feedback rápido, iteración

2. **Prototipo Alta Fidelidad**: Figma interactivo
   - Usability testing
   - Tareas específicas
   - Métricas: tasa éxito, tiempo, SUS Score

3. **MVP Funcional**: Implementación básica
   - Piloto con usuarios reales
   - Métricas reales
   - Casos de uso reales

### Pruebas de Aceptación (UAT)

**Plan UAT**:

- **Duración**: 1 semana
- **Participantes**: Médicos endocrinólogos

**Casos de Prueba**:

1. **Flujo Completo**: Buscar paciente, calcular predicción, exportar
2. **Datos Incompletos**: Validar manejo errores
3. **Validación Clínica**: Panel médicos revisa concordancia

**Criterios Éxito**:
- Tasa aprobación >90%
- Satisfacción usuarios >8/10
- Bugs críticos: 0

### Sprint Reviews

**Estructura**:
- Demo funcionalidades nuevas
- Feedback stakeholders
- Votación aceptación
- Planificación siguiente sprint

**Participantes**:
- Product Owner, Scrum Master, Equipo Dev
- Stakeholders: Médicos, CTO, Regulatorio, Inversores

---

## Checklist V&V ReMedical

**VERIFICACIÓN**:
- Conformidad especificaciones (algoritmo, tiempo, precisión)
- Cumplimiento regulatorio (FDA, HIPAA, ISO 13485)
- Estándares codificación (PEP 8, coverage >80%)
- Interoperabilidad (FHIR, API REST)

**VALIDACIÓN**:
- Validación clínica (panel médicos, concordancia)
- Usabilidad (SUS Score, tiempo aprendizaje)
- Impacto workflow (tiempo ahorrado, detección riesgos)
- Validación ética (consentimiento, equidad, transparencia)

### Matriz de Trazabilidad

| Requisito | Historia | Tests Unitarios | Tests UAT |
|-----------|----------|-----------------|-----------|
| Predicción <3seg | Dashboard UI | Cobertura >80% | UAT funcional |
| Modelo ML >90% | Modelo XGBoost | Cobertura >80% | Validación médica |
| Integración EHR | API FHIR | Cobertura >70% | Piloto hospital |

**Objetivo**: 100% requisitos con tests, 100% verificados, >90% validados

---

## Herramientas

| Categoría | Herramientas |
|-----------|--------------|
| **Gestión Requisitos** | Jira, Confluence, IBM DOORS |
| **Testing Funcional** | Pytest, Jest, Selenium, Postman |
| **Testing No Funcional** | JMeter, OWASP ZAP, Lighthouse |
| **Análisis Estático** | SonarQube, ESLint, Black |
| **Validación Médica** | Jupyter, SHAP, Tableau |
| **Cumplimiento** | Veracode, GitHub Actions |

---

## Mejores Prácticas

**DOs**:
- V&V desde día 1
- Involucrar usuarios reales
- Automatizar testing
- Documentar decisiones
- Medir métricas (defect density, coverage)

**DON'Ts**:
- Confundir verificación con validación
- V&V solo al final
- Ignorar requisitos no funcionales
- Falta de trazabilidad
- Omitir validación clínica (healthcare)


