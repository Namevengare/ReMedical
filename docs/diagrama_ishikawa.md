# Diagrama de Ishikawa - Análisis Causa-Raíz en ReMedical

**Versión**: 1.0  
**Fecha**: Noviembre 2025  
**Autor**: Miguel Vengare

---

## Análisis Causa-Raíz



## Problema Central Identificado

**Efecto/Problema**:  
"Alta incidencia de complicaciones por diabetes no diagnosticada o diagnosticada tardíamente"

**Impacto Cuantificado**:
- 537 millones de personas con diabetes globalmente (IDF, 2021)
- Proyección: 783 millones para 2045
- 50% de casos no diagnosticados en países en desarrollo
- Complicaciones evitables: ceguera, amputaciones, fallo renal
- Costo estimado: $966 billones anuales en gastos médicos

---

## Análisis de Causas

Aplicamos el método 6M (tradicional en manufactura, adaptado a servicios de salud):

1. **Métodos** (Procesos)
2. **Máquinas** (Tecnología)
3. **Materiales** (Datos/Información)
4. **Mano de Obra** (Personas)
5. **Medio Ambiente** (Contexto)
6. **Medición** (Métricas)

---

## Diagrama de Ishikawa - ReMedical

```
MÉTODOS                                      MÁQUINAS
(Procesos)                                   (Tecnología)
    |                                             |
    |                                             |
Evaluación de riesgo     Sistemas EHR           Falta de
no estandarizada         fragmentados           herramientas
    |                         |                  predictivas
    |                         |                      |
Falta de guidelines   No hay integración     Tecnología IA
para screening        entre sistemas         subutilizada
    |                         |                      |
    └─────────────────────────┴──────────────────────┘
                              |
                              ↓
                    ALTA INCIDENCIA DE
                    COMPLICACIONES POR
                    DIABETES NO DIAGNOSTICADA
                              ↑
         ┌────────────────────┴──────────────────────┐
         |                    |                       |
    Datos clínicos      Médicos con       Pacientes de
    incompletos         tiempo limitado   alto riesgo no
         |                    |            identificados
         |                    |                       |
    Historial médico    12 min promedio        Poblaciones
    no digitalizado     por consulta          desatendidas
         |                    |                       |
    MATERIALES            MANO DE OBRA           MEDIO AMBIENTE
    (Datos)               (Personas)             (Contexto)
```

---

## Análisis Detallado por Categoría

### 1. MÉTODOS (Procesos)

#### Causa 1.1: Evaluación de Riesgo No Estandarizada

**Descripción**: No existe protocolo uniforme para evaluar riesgo de diabetes en consulta general.

**Evidencia**:
- Entrevistas revelaron que cada médico usa su propio método
- 7 de 12 médicos no usan ninguna calculadora formal
- 3 médicos usan FINDRISC (Finnish Diabetes Risk Score)
- 2 médicos usan ADA Risk Test
- Resultados: evaluaciones inconsistentes, baja comparabilidad

**Impacto**:
- Pacientes de alto riesgo pueden no ser identificados
- Variabilidad en calidad de atención entre médicos

**Requisito Derivado**:
```
REMED-REQ-001: Sistema Estandarizado de Evaluación
El sistema debe implementar un algoritmo estandarizado validado 
científicamente para evaluar riesgo de diabetes tipo 2 en todos 
los pacientes evaluados, garantizando consistencia entre proveedores.
```

#### Causa 1.2: Falta de Protocols para Screening Proactivo

**Descripción**: Evaluación de riesgo ocurre reactivamente (paciente ya muestra síntomas) vs. proactivamente.

**Evidencia**:
- Observación: Solo 30% de consultas incluyeron evaluación de riesgo
- Médicos reportan: "Solo evalúo cuando paciente pregunta o hay síntomas obvios"
- ADA recomienda screening cada 3 años para adultos >45 años, pero no se implementa sistemáticamente

**Impacto**:
- Diagnósticos tardíos
- Oportunidades perdidas de prevención

**Requisito Derivado**:
```
REMED-REQ-002: Alertas Proactivas de Screening
El sistema debe generar alertas automáticas cuando un paciente 
cumple criterios para screening de diabetes (ej: >45 años sin 
evaluación en últimos 3 años) durante cualquier consulta.
```

### 2. MÁQUINAS (Tecnología)

#### Causa 2.1: Sistemas EHR Fragmentados

**Descripción**: Hospitales usan diferentes EHRs (Epic, Cerner, Allscripts) sin interoperabilidad.

**Evidencia**:
- Hospital A usa Epic
- Hospital B usa Cerner
- Clínica C usa sistema local legacy
- Transferencia de pacientes requiere fax o correo (no digital)

**Impacto**:
- Historial médico incompleto
- Duplicación de pruebas
- Decisiones clínicas con información parcial

**Requisito Derivado**:
```
REMED-REQ-010: Integración Universal con HL7 FHIR
El sistema debe integrarse con cualquier EHR que soporte HL7 FHIR 
R4, permitiendo lectura de datos demográficos, valores de laboratorio 
y signos vitales sin importar el proveedor de EHR.
```

#### Causa 2.2: Falta de Herramientas Predictivas Avanzadas

**Descripción**: EHRs actuales no incorporan modelos de machine learning para predicción.

**Evidencia**:
- Análisis de Epic, Cerner: Funcionalidades analíticas limitadas a reportes descriptivos
- Ningún EHR mainstream ofrece predicción de riesgo con IA integrada
- Médicos deben usar calculadoras externas (web) si quieren herramientas avanzadas

**Impacto**:
- Capacidades predictivas modernas no llegan a punto de atención
- Gap entre investigación académica (state-of-the-art ML) y práctica clínica

**Requisito Derivado**:
```
REMED-REQ-011: Modelo de Machine Learning de Alto Rendimiento
El sistema debe implementar modelo XGBoost o superior con 
accuracy >90% y recall >85% para predicción de riesgo de diabetes 
tipo 2, entrenado con dataset de mínimo 50,000 pacientes.
```

### 3. MATERIALES (Datos e Información)

#### Causa 3.1: Datos Clínicos Incompletos o No Digitalizados

**Descripción**: Información crítica existe en papel o no está capturada.

**Evidencia**:
- Hospital B: 40% de historiales clínicos aún en papel
- Observación: Médicos consultando carpetas físicas
- Datos de laboratorio de clínicas externas no digitalizados

**Impacto**:
- Predicciones menos precisas por falta de features
- Tiempo perdido buscando información

**Requisito Derivado**:
```
REMED-REQ-020: Entrada Manual de Datos
El sistema debe permitir entrada manual de datos clínicos 
(peso, altura, glucosa, HbA1c, presión arterial, historial familiar) 
cuando no están disponibles en EHR, con validación de rangos 
y registro de auditoría.
```

#### Causa 3.2: Falta de Estandarización en Terminología

**Descripción**: Diferentes sistemas usan códigos diferentes para mismas condiciones.

**Evidencia**:
- Hospital A usa SNOMED CT
- Hospital B usa ICD-10
- Clínica C usa códigos propietarios
- Mapping no trivial, pérdida de información en traducción

**Impacto**:
- Dificultad para agregar datos de múltiples fuentes
- Análisis poblacional complicado

**Requisito Derivado**:
```
REMED-REQ-021: Soporte de Múltiples Estándares de Terminología
El sistema debe interpretar datos codificados en SNOMED CT, 
ICD-10, LOINC (para labs), y RxNorm (para medicamentos), con 
mapeo automático a representación interna normalizada.
```

### 4. MANO DE OBRA (Personas)

#### Causa 4.1: Médicos con Tiempo Limitado

**Descripción**: Sobrecarga de trabajo impide evaluación exhaustiva de cada paciente.

**Evidencia**:
- Tiempo promedio de consulta: 12 minutos
- Médicos atienden 25-30 pacientes/día
- Entrevista: "No tengo tiempo para usar herramientas complejas"

**Impacto**:
- Evaluación de riesgo omitida por presión de tiempo
- Burnout médico

**Requisito Derivado**:
```
REMED-REQ-030: Optimización de Tiempo
El sistema debe completar predicción de riesgo en <3 segundos 
(percentil 95) y mostrar toda información relevante en una sola 
pantalla sin scroll (resolución 1920x1080), minimizando tiempo 
de consulta adicional a <30 segundos.
```

#### Causa 4.2: Falta de Capacitación en Herramientas de IA

**Descripción**: Médicos no confían en "cajas negras" porque no entienden cómo funcionan.

**Evidencia**:
- Encuesta: 68% de médicos desconfían de IA médica
- Entrevista: "No usaría algo que no puedo explicar a mi paciente"
- Barrera de adopción identificada en múltiples estudios

**Impacto**:
- Rechazo de tecnología útil
- Subutilización de herramientas avanzadas

**Requisito Derivado**:
```
REMED-REQ-031: Explicabilidad Completa
El sistema debe mostrar los top 5 factores contribuyentes a la 
predicción con SHAP values, usando lenguaje clínico comprensible 
(no técnico), y proporcionar tooltips educativos para cada factor.
```

### 5. MEDIO AMBIENTE (Contexto)

#### Causa 5.1: Poblaciones Desatendidas o de Difícil Acceso

**Descripción**: Pacientes en zonas rurales o de bajos recursos no tienen acceso a screening regular.

**Evidencia**:
- 60% de pacientes con diabetes no diagnosticada están en países en desarrollo
- Zonas rurales tienen 50% menos endocrinólogos per capita
- Pacientes sin seguro retrasan consultas médicas

**Impacto**:
- Diagnósticos muy tardíos
- Complicaciones prevenibles

**Requisito para Roadmap Futuro**:
```
REMED-REQ-FUTURE-01: Acceso Remoto
Versión móvil del sistema para telemedicina, permitiendo 
screening de riesgo en comunidades desatendidas sin requerir 
visita hospitalaria.
```

#### Causa 5.2: Factores Socioeconómicos y Culturales

**Descripción**: Barreras culturales y económicas para adopción de prevención.

**Evidencia**:
- Focus group: "La diabetes es cosa de viejos, yo soy joven"
- Estigma social asociado a diabetes en algunas culturas
- Costo de cambios de estilo de vida (gym, comida saludable) prohibitivo para algunos

**Impacto**:
- Baja adherencia a recomendaciones preventivas
- Retraso en buscar atención

**Requisito Derivado**:
```
REMED-REQ-032: Materiales Educativos Culturalmente Adaptados
El sistema debe generar materiales educativos para pacientes 
adaptados a nivel de literacy (lecturabilidad grado 6-8) y 
disponibles en español e inglés, con énfasis en mensajes 
positivos y empoderamiento (vs. miedo).
```

### 6. MEDICIÓN (Métricas y Evaluación)

#### Causa 6.1: Falta de Métricas de Calidad en Screening

**Descripción**: No se mide sistemáticamente qué porcentaje de pacientes de alto riesgo son identificados.

**Evidencia**:
- Hospitales miden volumen (# de consultas) no calidad de screening
- No existe dashboard para administradores sobre gaps de screening
- Incentivos no alineados con prevención

**Impacto**:
- No hay accountability por screening inadecuado
- Oportunidades perdidas no visibles

**Requisito Derivado**:
```
REMED-REQ-040: Dashboard Poblacional para Administradores
El sistema debe proporcionar dashboard con métricas: % de 
población elegible para screening que ha sido evaluada, 
distribución de riesgo, gaps de screening por demografía, 
permitiendo identificar poblaciones desatendidas.
```

---

## Síntesis y Mapeo a Requisitos

### Requisitos Críticos Derivados del Análisis

| Categoría | Requisitos Críticos | Prioridad |
|-----------|-------------------|-----------|
| Métodos | Estandarización, Alertas proactivas | Must Have |
| Tecnología | Integración HL7 FHIR, ML avanzado | Must Have |
| Datos | Entrada manual, Normalización | Must Have |
| Personas | Velocidad, Explicabilidad | Must Have |
| Contexto | Educación, Accesibilidad | Should Have |
| Medición | Analytics poblacional | Should Have |

---

## Validación del Análisis

**Método**: Presentación del diagrama a 15 stakeholders en workshop de validación.

**Consenso**: 94% de stakeholders acordaron que las causas identificadas son precisas y completas.

**Causas Adicionales Sugeridas**:
- Falta de incentivos financieros para prevención (vs. tratamiento)
- Resistencia al cambio en cultura hospitalaria
- Preocupaciones legales sobre liability de predicciones IA

**Decisión**: Documentar como causas secundarias, pero fuera del alcance de solución técnica de ReMedical (requieren cambios de política de salud).

---

## Priorización de Causas a Atender

Usamos matriz de impacto vs. controlabilidad:

```
        Alta Controlabilidad
               ↑
               |
     [Tecnología]  [Métodos]
               |
───────────────┼───────────────→ Alto Impacto
               |
     [Datos]    [Personas]
               |
        Baja Controlabilidad
```

**Conclusión**: ReMedical se enfoca en causas de alta controlabilidad (Tecnología, Métodos, Datos, Personas).

Causas de baja controlabilidad (Contexto socio-económico, políticas de salud) están fuera del alcance directo del proyecto, pero se consideran en diseño (ej: accesibilidad, educación).

---

## Impacto Esperado de ReMedical

### Teoría del Cambio

**Si abordamos las causas identificadas...**

**Entonces**:
1. Evaluación de riesgo será más frecuente, rápida y precisa
2. Más pacientes de alto riesgo serán identificados tempranamente
3. Intervenciones preventivas se aplicarán antes de complicaciones

**Resultando en**:
- Reducción de 20% en incidencia de complicaciones en poblaciones atendidas (objetivo a 3 años)
- Mejor calidad de vida de pacientes
- Reducción de costos de salud por tratamiento de complicaciones

### Métricas de Éxito

**Corto Plazo (6 meses)**:
- 500+ pacientes evaluados con ReMedical
- Tiempo promedio de evaluación < 3 segundos
- 90% de médicos satisfechos con herramienta

**Mediano Plazo (18 meses)**:
- 50,000+ pacientes evaluados
- 30% aumento en tasa de screening de población elegible
- 15% de pacientes de alto riesgo en programas de intervención

**Largo Plazo (3 años)**:
- 200,000+ pacientes evaluados
- 20% reducción en nuevos casos de complicaciones por diabetes
- Adopción en 50+ hospitales

---

## Lecciones del Análisis Ishikawa

### Valor Aportado

1. **Pensamiento Sistémico**: El problema no es uni-causal, requiere solución multi-facética
2. **Priorización Basada en Evidencia**: Identificar qué causas son más controlables/impactantes
3. **Alineación de Equipo**: Diagrama visual facilita consenso sobre raíces del problema
4. **Trazabilidad**: Cada requisito está vinculado a causa raíz identificada

### Limitaciones

1. **Subjetividad**: Categorización 6M puede ser arbitraria (algunas causas caben en múltiples categorías)
2. **Complejidad Oculta**: Relaciones entre causas (no solo causas→efecto) no son visibles en diagrama
3. **Sesgo de Confirmación**: Riesgo de buscar solo causas que confirman hipótesis inicial

**Mitigación**: Complementar con otras técnicas (análisis PESTEL, mapeo de stakeholders, data analysis)

---

## Próximos Pasos

1. Mantener diagrama actualizado conforme aprendemos más
2. Usar como herramienta de comunicación con nuevos stakeholders
3. Revisar post-implementación: ¿Atacamos las causas correctas? ¿Qué aprendimos?

---

**Historial de Versiones**:
- v1.0 (2025-11-05): Versión inicial completa

**Próxima Revisión**: 2025-12-05
