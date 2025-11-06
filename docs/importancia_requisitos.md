# Importancia de la Recolección de Requisitos

**Documento**: 02 - Fundamentos  
**Versión**: 1.0  
**Fecha**: Noviembre 2025  
**Autor**: Miguel Vengare

---

## Impacto Económico

**Estadísticas Clave**:
- 37% proyectos fallan por requisitos mal definidos (Standish Group, 2020)
- Costo de corrección aumenta 100x de requisitos a producción
- 70% del retrabajo por requisitos incorrectos

**Modelo de Costos** (Boehm, 2001):
```
Requisitos: $1 | Diseño: $5 | Implementación: $10 | Pruebas: $50 | Producción: $100-200
```

### Caso Real: HealthCare.gov (2013)

El lanzamiento fallido de HealthCare.gov es un ejemplo notorio:

**Problemas de Requisitos**:
- Requisitos cambiantes hasta semanas antes del lanzamiento
- Falta de claridad en requisitos de integración con aseguradoras
- Requisitos de seguridad subestimados
- No se validaron requisitos con usuarios reales

**Consecuencias**:
- Costo inicial: $93 millones USD
- Costo de corrección: $1,700 millones USD adicionales
- 6 meses de retraso
- Daño reputacional incalculable

**Lección para ReMedical**: Inversión upfront en requisitos hubiera ahorrado millones

---

## Impacto en la Calidad del Producto

### Satisfacción del Usuario

Un estudio de PMI (2018) encontró que proyectos con excelente gestión de requisitos tienen:

- 71% de satisfacción de stakeholders vs. 32% en proyectos con gestión deficiente
- 58% más probabilidad de cumplir objetivos de negocio
- 50% menos solicitudes de cambio post-implementación

### Alineación con Necesidades Reales

**Ejemplo en ReMedical**:

**Requisito Inicial** (basado en supuestos):
"El sistema debe mostrar gráficos avanzados de tendencias de riesgo a lo largo del tiempo"

**Requisito Validado** (tras entrevistas con 12 médicos):
"El sistema debe mostrar el riesgo actual en formato simple (bajo/medio/alto) con código de colores, y permitir acceso opcional a detalles históricos"

**Impacto**: Simplificación de UI, reducción de 3 semanas de desarrollo, mejor adopción por usuarios

---

## Impacto Regulatorio y Legal

### Sistemas Médicos y Responsabilidad

En el dominio de software médico, requisitos mal especificados pueden tener consecuencias legales graves:

**FDA Class II Medical Device** (categoría de ReMedical):
- Requiere documentación exhaustiva de requisitos
- Trazabilidad completa desde requisitos hasta casos de prueba
- Validación formal con evidencia documentada

**HIPAA Compliance**:
- Requisitos de privacidad deben estar explícitos y verificables
- Violaciones pueden costar hasta $1.5 millones anuales por categoría
- Responsabilidad civil y penal para ejecutivos

**Ejemplo de Requisito Crítico en ReMedical**:

```
REMED-SEC-001: Encriptación de Datos PHI
Descripción: Todos los datos de información de salud protegida (PHI) 
deben ser encriptados en tránsito usando TLS 1.3 y en reposo usando 
AES-256

Justificación Legal: HIPAA Security Rule §164.312(a)(2)(iv)
Criterio de Verificación: Auditoría de seguridad con herramientas 
automatizadas (OWASP ZAP, SSL Labs)
Consecuencia de Incumplimiento: Multa de $50,000 por violación, 
hasta $1.5M anuales
```

---

## Impacto en el Desarrollo Ágil

### Mito: "Agile no necesita requisitos detallados"

**Realidad**: Agilidad requiere requisitos claros, solo que expresados y refinados iterativamente.

**Prácticas Ágiles en ReMedical**:

1. **Product Backlog Refinement**: 10% del tiempo de sprint dedicado a clarificar requisitos
2. **Definition of Ready**: Historia no entra en sprint sin criterios de aceptación claros
3. **User Story Mapping**: Visualización de flujo completo antes de implementación

**Comparación de Enfoques**:

| Aspecto | Waterfall Tradicional | Ágil en ReMedical |
|---------|----------------------|-------------------|
| Momento de detalle | Todo upfront | Just-in-time |
| Formato | SRS de 200 páginas | Historias + criterios de aceptación |
| Validación | Al final | Cada sprint |
| Cambios | Costosos y formales | Esperados y gestionados |
| Participación stakeholders | Inicio y final | Continua |

---

## Técnicas de Recolección Aplicadas en ReMedical

### 1. Entrevistas Estructuradas

**Realizadas**: 12 entrevistas con médicos endocrinólogos  
**Duración**: 60-90 minutos cada una  
**Formato**: Semi-estructurado con guía de preguntas

**Muestra de Preguntas**:
- "Descríbame su flujo de trabajo típico al evaluar riesgo de diabetes en un paciente nuevo"
- "¿Qué información considera más crítica para tomar una decisión clínica?"
- "¿Qué le gustaría poder hacer que actualmente no puede con sus herramientas?"

**Resultado**: 23 requisitos funcionales, 8 requisitos de usabilidad

### 2. Observación Contextual

**Tiempo invertido**: 20 horas observando consultas médicas  
**Hospitales**: 2 instituciones diferentes

**Insights Clave**:
- Médicos tienen en promedio 12 minutos por consulta
- Usan sistemas EHR legados con interfaces complejas
- Frecuentemente deben consultar múltiples pantallas para tomar decisión

**Requisito Emergente**:
"El dashboard debe mostrar toda la información crítica en una sola pantalla sin necesidad de scroll para resolución 1920x1080"

### 3. Workshops Multidisciplinarios

**Participantes**: Médicos, enfermeras, administradores, desarrolladores, arquitectos  
**Sesiones**: 4 workshops de 3 horas

**Técnicas Utilizadas**:
- Brainstorming de funcionalidades deseadas
- Dot voting para priorización
- Storyboarding de flujos de usuario
- Análisis de pain points actuales

**Outcome**: Roadmap priorizado a 18 meses, 47 historias de usuario iniciales

### 4. Análisis de Literatura Científica

**Papers Revisados**: 34 estudios sobre predicción de diabetes con ML  
**Guidelines Consultadas**: ADA (American Diabetes Association) Standards of Care

**Requisitos Derivados**:
- Variables clínicas a incluir en modelo (glucosa, HbA1c, IMC, etc.)
- Umbrales de riesgo clínicamente relevantes
- Métricas de evaluación aceptadas (sensitivity, specificity)

### 5. Análisis Competitivo

**Sistemas Evaluados**: 7 plataformas de predicción de riesgo médico

**Análisis**:
- Fortalezas a emular
- Debilidades a evitar
- Gaps en el mercado (oportunidades)

**Ejemplo de Diferenciación**:
Competidores mostraban solo porcentaje de riesgo. ReMedical añade explicabilidad (SHAP values) para aumentar confianza médica.

---

## El Costo de NO Recolectar Requisitos Adecuadamente

### Escenario Hipotético: ReMedical sin Gestión de Requisitos

**Supuestos**:
- Equipo comienza a codificar basándose en idea inicial vaga
- No se valida con stakeholders médicos
- No se consideran requisitos regulatorios

**Consecuencias Probables**:

1. **Semana 8**: Equipo descubre que algoritmo elegido no cumple estándares FDA
   - Costo: 3 semanas de retrabajo ($45,000)

2. **Semana 16**: Demo a médicos revela que UI es confusa y no se ajusta a flujo clínico
   - Costo: 4 semanas de rediseño ($60,000)

3. **Semana 24**: Auditoría HIPAA identifica 12 violaciones de seguridad
   - Costo: 6 semanas de corrección + multa potencial ($90,000 + $50,000)

4. **Semana 32**: Integración con EHR falla porque no se especificaron protocolos (HL7 FHIR)
   - Costo: 5 semanas adicionales ($75,000)

**Costo Total**: $320,000 + 18 semanas de retraso  
**Costo de Oportunidad**: Competidor lanza producto similar primero

### Escenario Real: ReMedical con Gestión Rigurosa

**Inversión en Requisitos**:
- 340 horas-persona en recolección, análisis, validación
- Costo: $34,000 (10% del presupuesto inicial)

**Beneficios Medidos**:
- Solo 3 requisitos requirieron cambio mayor post-implementación
- Aprobación FDA en primer intento
- Zero violaciones HIPAA en auditoría
- 89% de satisfacción de usuarios en UAT

**ROI**: 380%

---

## Requisitos como Herramienta de Comunicación

### Stakeholders Diversos en ReMedical

| Stakeholder | Interés en Requisitos | Formato Preferido |
|-------------|----------------------|-------------------|
| Médicos | Funcionalidad clínica, usabilidad | Prototipos, casos de uso |
| Pacientes | Privacidad, accesibilidad | Lenguaje simple, FAQs |
| Desarrolladores | Especificaciones técnicas | SRS, diagramas UML |
| QA | Criterios de verificación | Casos de prueba, métricas |
| Reguladores | Cumplimiento normativo | Evidencia documental, trazabilidad |
| Inversores | ROI, time-to-market | Roadmap, métricas de negocio |

### Lenguaje Común: El Glosario

ReMedical mantiene un glosario de 150 términos que sirve como diccionario compartido:

**Ejemplo**:
- **HbA1c**: Hemoglobina glucosilada, medida promedio de glucosa sanguínea en últimos 3 meses. Normal: <5.7%, Prediabetes: 5.7-6.4%, Diabetes: ≥6.5%
- **PHI (Protected Health Information)**: Información de salud identificable protegida bajo HIPAA

---

## Requisitos y Gestión de Riesgos

### Identificación Temprana de Riesgos

Requisitos bien recolectados permiten identificar riesgos antes de invertir en desarrollo:

**Riesgos Identificados en ReMedical**:

1. **Riesgo Técnico**: Dataset de entrenamiento insuficiente
   - Mitigación: Alianza con hospital universitario para acceso a 50K registros anónimos

2. **Riesgo Regulatorio**: Posible reclasificación a FDA Class III (más estricto)
   - Mitigación: Asesor regulatorio, documentación exhaustiva desde día 1

3. **Riesgo de Adopción**: Resistencia de médicos a "caja negra" de IA
   - Mitigación: Requisito de explicabilidad (SHAP values), capacitación extensa

4. **Riesgo de Integración**: Variabilidad en sistemas EHR de hospitales
   - Mitigación: Adopción de estándar HL7 FHIR, capa de abstracción

---

## Métricas de Éxito en Recolección de Requisitos

### Métricas Aplicadas en ReMedical

**Cobertura**:
- Stakeholders entrevistados: 12 de 12 identificados (100%)
- Requisitos vinculados a objetivos de negocio: 100%

**Calidad**:
- Requisitos ambiguos en primera revisión: 8 de 60 (13%)
- Requisitos ambiguos en segunda revisión: 0 de 60 (0%)

**Estabilidad**:
- Volatilidad de requisitos: 23% (aceptable para proyecto ágil)
- Requisitos eliminados: 5% (bajo)

**Validación**:
- Participación de stakeholders en revisiones: 92% de convocados
- Satisfacción en UAT: 89%

---

## Lecciones Aprendidas en ReMedical

### Lo que Funcionó Bien

1. **Involucramiento Continuo**: Sesiones quincenales con médicos mantuvieron alineación
2. **Prototipos Rápidos**: Validación visual previno malentendidos
3. **Documentación Viva**: Confluence permitió actualización continua sin "documentos muertos"
4. **Trazabilidad**: Matriz mantuvo visibilidad de impacto de cambios

### Lo que Mejoraríamos

1. **Participación de Pacientes**: Solo incluidos tardíamente, hubieran aportado perspectiva valiosa
2. **Estimación Inicial**: Subestimamos tiempo de recolección en 30%
3. **Requisitos de Datos**: Calidad de datos del EHR fue mayor reto de lo anticipado

---

## Conclusiones

La recolección rigurosa de requisitos en ReMedical no fue un gasto, fue una inversión estratégica que:

- **Redujo riesgos** técnicos, regulatorios y de adopción
- **Alineó expectativas** entre stakeholders diversos
- **Facilitó estimación** precisa y planificación realista
- **Previno defectos** costosos en fases posteriores
- **Aumentó satisfacción** de usuarios finales

**Principio Fundamental**:  
"Invierte 10% de tu tiempo/presupuesto en requisitos para ahorrar 50% en retrabajo"

---

## Referencias

- Standish Group (2020). CHAOS Report
- Boehm, B. W. (2001). Software Engineering Economics
- PMI (2018). Pulse of the Profession: Requirements Management
- IEEE 830-1998: Recommended Practice for Software Requirements Specifications
- FDA Guidance on Medical Device Software

---

**Historial de Versiones**:
- v1.0 (2025-11-05): Versión inicial completa

**Próxima Revisión**: 2025-12-05
