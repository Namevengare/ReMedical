# Técnicas de Recolección de Requisitos - ReMedical

**Versión**: 1.0  
**Fecha**: Noviembre 2025  
**Autor**: Miguel Vengare

---



## Técnicas Aplicadas en ReMedical

### 1. Entrevistas Estructuradas

**Descripción**: Conversaciones uno-a-uno con stakeholders clave siguiendo una guía predefinida de preguntas pero permitiendo exploración de temas emergentes.

**Implementación en ReMedical**:

**Participantes Entrevistados**:
- 12 médicos endocrinólogos de 3 hospitales diferentes
- 3 administradores de salud poblacional
- 2 oficiales de compliance (HIPAA/FDA)
- 4 enfermeras especializadas en diabetes

**Duración**: 60-90 minutos por entrevista  
**Formato**: Semi-estructurado con guía flexible  
**Grabación**: Audio (con consentimiento) para análisis posterior

**Guía de Entrevista - Médicos Endocrinólogos**:

```
SECCIÓN 1: Contexto y Flujo de Trabajo Actual (15 min)
1. Descríbame un día típico en su consulta
2. ¿Cuántos pacientes atiende en promedio por día?
3. ¿Cuánto tiempo dedica a evaluar riesgo de diabetes en pacientes nuevos?
4. ¿Qué herramientas o sistemas utiliza actualmente?

SECCIÓN 2: Proceso de Evaluación de Riesgo (20 min)
5. ¿Qué factores considera más importantes al evaluar riesgo de diabetes?
6. ¿Utiliza algún score o calculadora actualmente? (ej: FINDRISC, ADA Risk Test)
7. ¿Qué información le gustaría tener que actualmente no tiene fácilmente disponible?
8. ¿Cómo comunica el riesgo a sus pacientes?

SECCIÓN 3: Pain Points y Necesidades (20 min)
9. ¿Cuáles son los mayores desafíos que enfrenta al evaluar riesgo de diabetes?
10. ¿Qué le tomaría más tiempo de lo que quisiera?
11. Si pudiera tener una herramienta mágica, ¿qué haría?
12. ¿Ha usado sistemas de IA médica antes? ¿Qué le gustó/disgustó?

SECCIÓN 4: Requisitos Específicos (15 min)
13. ¿Qué nivel de precisión esperaría de una herramienta de predicción?
14. ¿Qué tan importante es entender "por qué" el sistema da cierto resultado?
15. ¿Cómo le gustaría que se presentara la información? (gráficos, números, texto)
16. ¿Qué integraciones con otros sistemas necesitaría?

SECCIÓN 5: Adopción y Capacitación (10 min)
17. ¿Cuánto tiempo tendría disponible para capacitación en una nueva herramienta?
18. ¿Qué haría que usted NO adopte una nueva tecnología?
19. ¿Quién más en su equipo usaría esta herramienta?
```

**Insights Clave Obtenidos**:

1. **Tiempo es Crítico**: Médicos tienen en promedio 12 minutos por consulta
   - Requisito: Sistema debe ser rápido (< 3 segundos para predicción)

2. **Confianza requiere Explicabilidad**: 11 de 12 médicos dijeron que no confiarían en "caja negra"
   - Requisito: Explicabilidad con SHAP values, mostrar factores contribuyentes

3. **Integración es Esencial**: Nadie quiere otro sistema aislado
   - Requisito: Integración HL7 FHIR con EHR existente

4. **Comunicación Visual**: Pacientes entienden mejor colores que números
   - Requisito: Código de colores (verde/amarillo/rojo) para niveles de riesgo

**Documentación Generada**:
- 12 transcripciones de entrevistas (220 páginas)
- Matriz de insights por tema
- 23 requisitos funcionales identificados
- 8 requisitos no funcionales emergentes

---

### 2. Observación Contextual (Shadowing)

**Descripción**: Observación directa de usuarios en su ambiente natural de trabajo sin intervención.

**Implementación en ReMedical**:

**Tiempo Invertido**: 20 horas distribuidas en:
- Hospital Universitario A: 8 horas (4 médicos)
- Hospital Comunitario B: 12 horas (6 médicos)

**Protocolo de Observación**:
1. Obtener consentimiento de médicos y pacientes
2. Posicionarse donde se pueda ver pantalla sin interrumpir
3. Tomar notas de campo sobre: flujo de trabajo, puntos de fricción, workarounds
4. Grabar tiempo de tareas clave (con cronómetro discreto)
5. No preguntar durante observación, debrief al final del día

**Hallazgos Inesperados**:

**Workaround Común**: Médicos tienen "cheat sheets" impresas con rangos de referencia
- **Insight**: EHR no muestra claramente si valor está fuera de rango
- **Requisito Emergente**: Resaltar valores anormales con código de colores

**Fragmentación de Datos**: Médicos deben abrir 4-5 pantallas diferentes del EHR para obtener información completa
- **Insight**: Tiempo perdido navegando sistemas
- **Requisito Emergente**: Dashboard unificado con toda info relevante en una vista

**Interrupción de Flujo**: Médicos frecuentemente olvidan documentar evaluación de riesgo
- **Insight**: Proceso actual requiere demasiados pasos
- **Requisito Emergente**: Integración transparente que documente automáticamente

**Uso de Calculadoras Externas**: 4 de 10 médicos observados usaron calculadora web externa (fuera del EHR)
- **Insight**: Herramientas actuales del EHR son inadecuadas
- **Requisito Emergente**: Embeber herramienta directamente en EHR workflow

**Métricas Observadas**:
- Tiempo promedio de consulta: 12.4 minutos
- Tiempo buscando información en EHR: 3.2 minutos (26% de consulta!)
- Número de clics para acceder a valores de laboratorio: 7-9 clics
- Documentación de evaluación de riesgo: solo 30% de casos

---

### 3. Workshops Multidisciplinarios

**Descripción**: Sesiones facilitadas donde stakeholders diversos colaboran para definir requisitos.

**Implementación en ReMedical**:

**Workshop 1: Visión y Alcance**
- **Fecha**: 15 de septiembre, 2025
- **Duración**: 3 horas
- **Participantes**: 15 personas (médicos, enfermeras, admin, arquitecto, PO, desarrolladores)
- **Objetivo**: Definir visión compartida y alcance del MVP

**Agenda**:
```
09:00 - 09:30: Bienvenida y contexto del proyecto
09:30 - 10:30: Brainstorming de funcionalidades deseadas (sticky notes)
10:30 - 10:45: Pausa
10:45 - 11:30: Agrupación de ideas por temas (affinity mapping)
11:30 - 12:00: Dot voting para priorización
```

**Técnica: Brainstorming con Sticky Notes**:
- Cada participante escribe ideas en post-its (1 idea por post-it)
- Sin críticas ni filtros en fase inicial
- 15 minutos de generación intensiva de ideas

**Resultado**: 87 ideas generadas inicialmente

**Técnica: Affinity Mapping**:
- Agrupar ideas similares en categorías
- Emergen temas naturales

**Categorías Emergentes**:
1. Predicción y Algoritmos (18 ideas)
2. Visualización y Dashboard (22 ideas)
3. Integración con EHR (15 ideas)
4. Reportes y Exportación (12 ideas)
5. Seguridad y Compliance (10 ideas)
6. Educación de Pacientes (10 ideas)

**Técnica: Dot Voting**:
- Cada participante tiene 5 votos (dots)
- Pueden asignar múltiples votos a una sola idea
- Ideas con más votos son prioritarias

**Top 5 Ideas Priorizadas**:
1. Predicción rápida y precisa de riesgo (23 votos)
2. Explicabilidad de la predicción (19 votos)
3. Integración transparente con EHR (18 votos)
4. Dashboard visual simple (17 votos)
5. Exportación de reporte PDF (14 votos)

**Workshop 2: Definición de Historias de Usuario**
- **Fecha**: 29 de septiembre, 2025
- **Duración**: 4 horas
- **Participantes**: 10 personas (PO, médicos clave, arquitecto, devs)

**Técnica: User Story Mapping**:

```
                ÉPICA 1: Acceso al Sistema
                        |
        ┌───────────────┼───────────────┐
        ↓               ↓               ↓
    Login SSO    Buscar Paciente   Ver Perfil
        |               |               |
    [Stories]       [Stories]       [Stories]


                ÉPICA 2: Predicción
                        |
        ┌───────────────┼───────────────┐
        ↓               ↓               ↓
 Calcular Riesgo  Ver Explicación  Ver Historial
        |               |               |
    [Stories]       [Stories]       [Stories]
```

**Resultado**: 47 historias de usuario escritas en formato estándar

**Workshop 3: Priorización con MoSCoW**
- **Fecha**: 6 de octubre, 2025
- **Duración**: 2 horas

**Técnica MoSCoW**:
- **Must Have**: Crítico para MVP, sin esto no hay valor
- **Should Have**: Importante pero no bloqueante
- **Could Have**: Deseable si hay tiempo
- **Won't Have**: Fuera de alcance de este release

**Resultado de Priorización**:
- Must Have: 28 historias (40% del backlog)
- Should Have: 24 historias (35%)
- Could Have: 14 historias (20%)
- Won't Have: 4 historias (5%)

---

### 4. Análisis de Documentación Existente

**Descripción**: Revisión de documentación, regulaciones, literatura científica y sistemas existentes.

**Fuentes Analizadas**:

**Literatura Científica**:
- 34 papers sobre predicción de diabetes con machine learning
- PubMed, Google Scholar, IEEE Xplore
- Criterios de selección: publicados post-2018, datasets >10K pacientes

**Insights Clave**:
- Variables más predictivas: HbA1c, glucosa en ayunas, IMC, edad, historial familiar
- Algoritmos más efectivos: XGBoost, Random Forest, Deep Neural Networks
- Accuracy reportado: 85-94% según dataset

**Guidelines Clínicos**:
- ADA Standards of Care 2025 (American Diabetes Association)
- IDF Guidelines (International Diabetes Federation)

**Requisitos Derivados**:
- Umbrales de riesgo deben alinearse con ADA guidelines
- Métricas de evaluación: sensitivity (recall) prioritario sobre accuracy (no queremos false negatives)

**Regulaciones**:
- FDA Guidance on Software as a Medical Device (SaMD)
- HIPAA Privacy and Security Rules
- 21 CFR Part 820 (Quality System Regulation)

**Requisitos de Compliance**:
- Documentación completa de diseño (Design History File)
- Trazabilidad de requisitos a tests
- Validación formal con evidencia
- Encriptación de PHI (AES-256)
- Logs de auditoría inmutables

**Sistemas Competidores Analizados**:
1. IBM Watson for Diabetes
2. Glooko Population Tracker
3. Livongo Health
4. MySugr PRO
5. HealthifyMe for Healthcare Providers

**Benchmark**:

| Feature | Competidor A | Competidor B | ReMedical (Target) |
|---------|-------------|-------------|-------------------|
| Tiempo de predicción | 5-7 seg | 3-5 seg | <3 seg |
| Explicabilidad | No | Básica | Avanzada (SHAP) |
| Integración EHR | Limitada | Epic only | HL7 FHIR (universal) |
| Costo por usuario/mes | $45 | $35 | $25 (target) |

**Gap Analysis**:
- Oportunidad: Ningún competidor ofrece explicabilidad avanzada
- Diferenciador: Enfoque en transparencia y confianza médica

---

### 5. Encuestas y Cuestionarios

**Descripción**: Recolección estructurada de datos cuantitativos de muestra amplia.

**Encuesta Post-Workshop**: 
- **Objetivo**: Validar prioridades con muestra más amplia
- **Participantes**: 45 médicos endocrinólogos (no pudieron asistir a workshops)
- **Plataforma**: Google Forms
- **Tasa de respuesta**: 78% (35 respuestas completas)

**Preguntas Clave**:

1. **Evalúe importancia de las siguientes funcionalidades** (escala 1-5):
   - Predicción de riesgo de diabetes: 4.8/5
   - Explicabilidad de predicción: 4.6/5
   - Integración con EHR: 4.9/5 (más alta!)
   - Dashboard de población: 3.8/5
   - Educación de pacientes: 3.2/5

2. **¿Qué tan preciso debe ser el sistema para que confíe en él?**
   - >95%: 12% de respuestas
   - >90%: 54% de respuestas (mayoría)
   - >85%: 31% de respuestas
   - >80%: 3% de respuestas

**Requisito Derivado**: Target de accuracy >90%

3. **¿Cuánto tiempo dedicaría a capacitación?**
   - <30 minutos: 40%
   - 30-60 minutos: 43%
   - 1-2 horas: 14%
   - >2 horas: 3%

**Requisito Derivado**: Tutorial interactivo de 15-30 minutos

---

### 6. Prototipado Rápido

**Descripción**: Creación de prototipos de baja y alta fidelidad para validar requisitos antes de implementación.

**Fase 1: Wireframes (Baja Fidelidad)**
- **Herramienta**: Balsamiq
- **Tiempo**: 1 semana
- **Pantallas**: 12 wireframes principales

**Técnica: Paper Prototyping**:
- Dibujar interfaces en papel
- Simular interacción con usuario (mover "pantallas" de papel)
- Muy rápido y económico para validar flujos

**Sesión de Validación**:
- 5 médicos evaluaron wireframes
- Think-aloud protocol: narrar qué piensan mientras navegan
- Identificación temprana de confusiones de UX

**Feedback Crítico**:
- "No encuentro dónde buscar paciente" → Agregar barra de búsqueda prominente
- "Mucha información en una pantalla, abrumador" → Simplificar, usar tabs
- "El botón de predicción no es obvio" → Hacer más grande y con color distintivo

**Fase 2: Prototipos Interactivos (Alta Fidelidad)**
- **Herramienta**: Figma
- **Tiempo**: 3 semanas
- **Pantallas**: 23 diseños completos con flujos interactivos

**Validación**:
- 8 médicos completaron 5 tareas predefinidas
- Métricas: tiempo de tarea, tasa de éxito, errores

**Resultados**:
- Tarea 1 (Buscar paciente): 100% éxito, 18 seg promedio
- Tarea 2 (Calcular predicción): 100% éxito, 32 seg promedio
- Tarea 3 (Entender factores): 87% éxito (1 usuario confundido)
- Tarea 4 (Exportar PDF): 100% éxito, 12 seg promedio

**Iteraciones**: 3 ciclos de diseño-validación-refinamiento antes de implementación

---

### 7. Focus Groups

**Descripción**: Discusión grupal moderada para explorar percepciones, opiniones y actitudes.

**Focus Group con Pacientes**:
- **Participantes**: 8 pacientes con pre-diabetes o alto riesgo
- **Duración**: 90 minutos
- **Objetivo**: Entender expectativas y preocupaciones sobre IA en salud

**Temas Explorados**:
1. Confianza en predicciones de IA
2. Privacidad de datos de salud
3. Comunicación de riesgo
4. Motivación para cambios de estilo de vida

**Insights**:
- **Temor a "caja negra"**: Pacientes quieren entender por qué tienen riesgo
  - Requisito: Explicación en lenguaje simple, no técnico
  
- **Privacidad como prioridad**: Preocupación sobre quién ve sus datos
  - Requisito: Transparencia en políticas de privacidad, consentimiento informado claro

- **Preferencia por visualización**: "Los números me asustan, prefiero ver gráficos"
  - Requisito: Visualización amigable con colores y gráficos simples

- **Contexto familiar**: "Mi papá tiene diabetes, ¿eso afecta mi riesgo?"
  - Requisito: Incluir historial familiar como factor explicado claramente

---

## Síntesis de Técnicas

### Matriz de Técnicas vs. Objetivos

| Técnica | Qué descubre | Cuándo usar | Costo | Tiempo |
|---------|-------------|------------|-------|--------|
| Entrevistas | Necesidades profundas, contexto | Temprano | Medio | Alto |
| Observación | Flujos reales, workarounds | Temprano/Medio | Bajo | Alto |
| Workshops | Consenso, priorización | Temprano | Alto | Medio |
| Análisis Documental | Requisitos regulatorios, benchmarks | Temprano | Bajo | Medio |
| Encuestas | Validación cuantitativa | Medio | Bajo | Bajo |
| Prototipos | Validación de UX/UI | Medio/Tardío | Medio | Medio |
| Focus Groups | Percepciones, actitudes | Temprano/Medio | Alto | Medio |

---

## Resultados Consolidados

### Requisitos Identificados por Técnica

| Técnica | RF Identificados | RNF Identificados |
|---------|-----------------|------------------|
| Entrevistas | 23 | 8 |
| Observación | 12 | 6 |
| Workshops | 18 | 4 |
| Análisis Documental | 8 | 12 |
| Encuestas | 3 | 2 |
| Prototipos | 5 | 3 |
| Focus Groups | 2 | 4 |
| **TOTAL** | **47** | **23** |

**Nota**: Algunos requisitos fueron identificados por múltiples técnicas (convergencia)

### Inversión de Tiempo

- Entrevistas: 28 horas (21 entrevistas × 1.3 horas promedio)
- Observación: 20 horas
- Workshops: 12 horas (4 sesiones × 3 horas)
- Análisis Documental: 60 horas
- Encuestas: 8 horas (diseño, distribución, análisis)
- Prototipado: 80 horas
- Focus Groups: 6 horas (2 sesiones × 3 horas)

**Total: 214 horas-persona en recolección**

**ROI Estimado**: 
- Inversión: $21,400 (214 hrs × $100/hr promedio)
- Defectos evitados: ~35 (basado en industry benchmarks)
- Costo de defecto en producción: $10,000 promedio
- Ahorro: $350,000 - $21,400 = **$328,600**

---

## Lecciones Aprendidas

### Lo que Funcionó Excelentemente

1. **Observación Contextual**: Reveló problemas que stakeholders no mencionaron en entrevistas (ej: fragmentación de datos)
2. **Prototipos Iterativos**: Validación temprana evitó retrabajos costosos
3. **Triangulación**: Usar múltiples técnicas dio confianza en requisitos

### Desafíos Enfrentados

1. **Acceso a Pacientes**: Complicado por requisitos éticos y logísticos
   - Solución: Focus groups pequeños con reclutamiento a través de médicos

2. **Lenguaje Técnico vs. Clínico**: Malentendidos frecuentes inicialmente
   - Solución: Glosario compartido, sesiones de educación mutua

3. **Expectativas No Realistas**: Stakeholders esperaban sistema perfecto
   - Solución: Educación sobre limitaciones de IA, énfasis en herramienta de apoyo (no reemplazo)

---

## Recomendaciones para Futuros Proyectos

1. **Invertir en Observación**: No confiar solo en lo que stakeholders dicen, observar lo que hacen
2. **Prototipar Temprano y Frecuentemente**: Imágenes valen más que palabras
3. **Incluir Usuarios Finales Reales**: No solo managers o proxies
4. **Documentar Exhaustivamente**: Grabaciones, transcripciones, notas de campo
5. **Validar Cuantitativamente**: Complementar insights cualitativos con encuestas

---

**Historial de Versiones**:
- v1.0 (2025-11-05): Versión inicial completa

**Próxima Revisión**: 2025-12-05
