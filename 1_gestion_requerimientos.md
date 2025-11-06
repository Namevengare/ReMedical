# Gestión de Requerimientos - ReMedical

## 1. Conceptos Básicos de Gestión de Requerimientos

### ¿Qué es un Requerimiento?
Un requerimiento es una declaración que especifica una necesidad o capacidad que debe satisfacer un sistema de software. Los requerimientos pueden ser:

- **Requerimientos Funcionales**: Describen lo que el sistema debe hacer
- **Requerimientos No Funcionales**: Describen cómo debe comportarse el sistema

### Tipos de Requerimientos

#### Requerimientos de Negocio
Definen las necesidades de alto nivel de la organización.
- **Ejemplo ReMedical**: "La plataforma debe acelerar el descubrimiento de medicamentos mediante IA"

#### Requerimientos de Usuario
Describen las tareas que los usuarios deben realizar.
- **Ejemplo ReMedical**: "Como investigador médico, necesito analizar datos de pacientes para identificar patrones de diabetes"

#### Requerimientos de Sistema
Especificaciones técnicas detalladas del sistema.
- **Ejemplo ReMedical**: "El sistema debe procesar 10 millones de registros de pacientes en menos de 5 minutos"

### Características de Buenos Requerimientos

Los requerimientos deben ser **SMART**:
- **S**pecific (Específicos)
- **M**easurable (Medibles)
- **A**chievable (Alcanzables)
- **R**elevant (Relevantes)
- **T**ime-bound (Limitados en tiempo)

## 2. Importancia de la Recolección de Requisitos

### ¿Por Qué es Crítica?

1. **Reduce Costos**: Corregir errores en requisitos cuesta 100x más en producción que en la fase de requisitos
2. **Evita Retrabajo**: El 70% de los proyectos fallidos tienen problemas de requisitos mal definidos
3. **Alinea Expectativas**: Asegura que todos los stakeholders tengan la misma visión
4. **Base para Testing**: Los requisitos son la base para crear casos de prueba

### Impacto en ReMedical

En el contexto de nuestro proyecto de desarrollo de medicamentos:
- **Cumplimiento Regulatorio**: La FDA requiere documentación precisa de requisitos
- **Seguridad del Paciente**: Requisitos mal definidos pueden comprometer la seguridad
- **Eficiencia en I+D**: Requisitos claros aceleran el desarrollo de compuestos químicos
- **Trazabilidad**: Permite seguir desde el requisito inicial hasta el medicamento final

### Consecuencias de Mala Recolección de Requisitos

| Problema | Impacto en ReMedical |
|----------|---------------------|
| Requisitos ambiguos | Desarrollo de algoritmos IA incorrectos |
| Requisitos incompletos | Falta de funcionalidades críticas para análisis médico |
| Requisitos inconsistentes | Conflictos entre módulos de predicción y tratamiento |
| Requisitos no validados | Rechazo por parte de médicos y reguladores |

## 3. Ciclo de Vida de Desarrollo de Software (SDLC)

### Modelo Cascada (Waterfall)
```
Requisitos → Diseño → Implementación → Pruebas → Despliegue → Mantenimiento
```

**Ventajas para ReMedical**: 
- Ideal para componentes con requisitos estables (análisis de datos históricos)
- Documentación exhaustiva requerida por FDA

**Desventajas**: 
- Poca flexibilidad para cambios en investigación médica

### Modelo Ágil (Agile/Scrum)
```
Sprint Planning → Daily Standups → Development → Sprint Review → Sprint Retrospective
↓                                                                              ↑
└──────────────────────────────────────────────────────────────────────────────┘
                              (Iteraciones de 2-4 semanas)
```

**Ventajas para ReMedical**:
- Adaptación rápida a nuevos descubrimientos médicos
- Entrega continua de valor (prototipos de dashboards IA)
- Feedback constante de médicos e investigadores

### Modelo DevOps
```
Plan → Code → Build → Test → Release → Deploy → Operate → Monitor
↓                                                                ↑
└────────────────────────────────────────────────────────────────┘
                    (Integración y Entrega Continua)
```

**Aplicación en ReMedical**:
- CI/CD para actualizaciones de modelos de IA
- Monitoreo continuo de predicciones de diabetes
- Despliegue rápido de nuevas funcionalidades

### Fases del SDLC Aplicadas a ReMedical

#### Fase 1: Análisis de Requisitos
- **Actividades**: Entrevistas con médicos, análisis de normativas FDA, revisión de literatura científica
- **Entregables**: Documento de Especificación de Requisitos (SRS)
- **Stakeholders**: Médicos, investigadores, pacientes, reguladores

#### Fase 2: Diseño
- **Actividades**: Arquitectura de microservicios, diseño de bases de datos big data, diseño de algoritmos IA
- **Entregables**: Diagramas UML, prototipos de UI, arquitectura técnica
- **Herramientas**: Figma, Draw.io, AWS Architecture Diagrams

#### Fase 3: Implementación
- **Actividades**: Desarrollo de módulos de IA, integración con EHR, desarrollo de dashboards
- **Tecnologías**: Python (TensorFlow/PyTorch), React, PostgreSQL, Apache Spark
- **Prácticas**: Programación en parejas, Code reviews, TDD

#### Fase 4: Pruebas
- **Tipos**: Unitarias, Integración, Sistema, Aceptación de Usuario (UAT)
- **Específico ReMedical**: Validación de modelos IA con datasets clínicos, pruebas de rendimiento con big data
- **Herramientas**: Pytest, Jest, Selenium, JMeter

#### Fase 5: Despliegue
- **Estrategias**: Blue-Green deployment, Canary releases
- **Infraestructura**: AWS/Azure cloud, Kubernetes para orquestación
- **Consideraciones**: Cumplimiento HIPAA, encriptación de datos de pacientes

#### Fase 6: Mantenimiento
- **Actividades**: Monitoreo de modelos IA, actualización de datasets, corrección de bugs
- **Métricas**: Uptime 99.9%, latencia <200ms, precisión de predicción >95%

## 4. Técnicas de Recolección de Requisitos

### 4.1 Entrevistas

**Descripción**: Conversaciones estructuradas o semi-estructuradas con stakeholders.

**Aplicación en ReMedical**:
- **Entrevistas con Médicos**: Identificar necesidades en diagnóstico de diabetes
- **Entrevistas con Investigadores**: Requisitos para análisis de compuestos químicos
- **Entrevistas con Pacientes**: Expectativas de personalización de tratamiento

**Ejemplo de Preguntas**:
```
1. ¿Qué información necesita visualizar en el dashboard de predicción de diabetes?
2. ¿Qué formatos de datos maneja actualmente en su práctica clínica?
3. ¿Cuánto tiempo dedica actualmente al análisis manual de datos de pacientes?
4. ¿Qué nivel de precisión considera aceptable para predicciones de IA?
```

**Ventajas**: Información detallada, clarificación inmediata de dudas
**Desventajas**: Consume tiempo, puede haber sesgos del entrevistador

### 4.2 Cuestionarios y Encuestas

**Descripción**: Recolección masiva de datos mediante preguntas estandarizadas.

**Aplicación en ReMedical**:
```markdown
**Encuesta a 500 Médicos Endocrinólogos**

1. ¿Utiliza herramientas digitales para seguimiento de pacientes diabéticos?
   [ ] Sí [ ] No [ ] A veces

2. ¿Qué funcionalidades priorizaría en una plataforma de IA médica? (Rankear 1-5)
   [ ] Predicción de riesgo de complicaciones
   [ ] Recomendación personalizada de tratamiento
   [ ] Análisis de adherencia a medicamentos
   [ ] Visualización de tendencias de glucosa
   [ ] Integración con wearables

3. ¿Qué tan importante es la integración con su sistema EHR actual?
   [ ] Crítico [ ] Importante [ ] Deseable [ ] No importante
```

**Ventajas**: Datos cuantitativos, alcance amplio, bajo costo
**Desventajas**: Respuestas superficiales, baja tasa de respuesta

### 4.3 Observación (Job Shadowing)

**Descripción**: Observar a usuarios en su entorno de trabajo real.

**Aplicación en ReMedical**:
- Observar consultas médicas para entender flujo de trabajo
- Ver cómo investigadores analizan datos de ensayos clínicos
- Estudiar interacciones paciente-médico

**Hallazgos Típicos**:
```
Observación: Médico tarda 15 minutos en buscar historial de paciente en 3 sistemas
→ Requisito: "El sistema debe consolidar datos de múltiples fuentes en vista unificada"

Observación: Investigadores exportan datos a Excel manualmente
→ Requisito: "Permitir exportación automatizada en formatos CSV, JSON y XLSX"
```

### 4.4 Talleres de Requisitos (Workshops)

**Descripción**: Sesiones colaborativas con múltiples stakeholders.

**Agenda Típica de Workshop ReMedical** (4 horas):
```
09:00-09:30: Presentación del proyecto y objetivos
09:30-10:30: Brainstorming de funcionalidades (Post-its)
10:30-10:45: Break
10:45-11:30: Priorización (MoSCoW: Must/Should/Could/Won't)
11:30-12:30: Definición de historias de usuario
12:30-13:00: Revisión y próximos pasos
```

**Técnicas Utilizadas**:
- Brainstorming
- Dot Voting (votación con puntos)
- Matriz de priorización (Urgencia vs Impacto)

### 4.5 Análisis de Documentación

**Descripción**: Revisar documentos existentes para extraer requisitos.

**Documentos Analizados en ReMedical**:
- **Normativas FDA**: 21 CFR Part 11 (registros electrónicos)
- **Guías Clínicas**: ADA Standards of Medical Care in Diabetes
- **Literatura Científica**: Papers sobre predicción de diabetes con ML
- **Sistemas Legacy**: Documentación de sistemas hospitalarios actuales
- **Leyes de Privacidad**: HIPAA, GDPR para datos de salud

**Ejemplo de Extracción**:
```
Documento: FDA 21 CFR Part 11
Texto: "Systems must use secure, computer-generated, time-stamped audit trails"
→ Requisito No Funcional: "El sistema debe generar logs auditables con timestamp 
   de todas las modificaciones a datos de pacientes"
```

### 4.6 Prototipos y Mockups

**Descripción**: Crear representaciones visuales tempranas del sistema.

**Tipos de Prototipos en ReMedical**:

1. **Prototipos de Baja Fidelidad** (Papel/Wireframes):
```
┌─────────────────────────────────────┐
│ ReMedical Dashboard       [Profile] │
├─────────────────────────────────────┤
│ [Buscar Paciente...]                │
├──────────────┬──────────────────────┤
│              │  Predicción Riesgo   │
│  Lista       │  Diabetes: 87% ALTO  │
│  Pacientes   │  ──────────────────  │
│  (100)       │  [Gráfico Glucosa]   │
│              │  [Recomendaciones]   │
└──────────────┴──────────────────────┘
```

2. **Prototipos de Alta Fidelidad** (Figma/Adobe XD):
- Diseño completo con colores, tipografías, interacciones
- Flujos completos de usuario
- Simulación de datos reales

**Validación con Usuarios**:
```
Test de Usabilidad (5 médicos):
- Tarea: "Encuentra el historial de medicación del paciente Juan Pérez"
- Métrica: Tiempo promedio = 12 segundos (objetivo: <15 seg) ✓
- Feedback: "Necesito ver dosis actuales más prominente"
→ Requisito: "Mostrar dosis actual de medicamentos en negrita"
```

### 4.7 Análisis de Competencia (Benchmarking)

**Descripción**: Estudiar sistemas similares en el mercado.

**Competidores Analizados**:
| Sistema | Fortalezas | Debilidades | Requisitos Derivados |
|---------|------------|-------------|---------------------|
| IBM Watson Health | IA avanzada | Costo alto | "Ofrecer pricing competitivo basado en uso" |
| Epic MyChart | Integración EHR | UI compleja | "Diseño intuitivo para usuarios no técnicos" |
| Glooko | Integración wearables | Solo diabetes | "Expandir a múltiples condiciones crónicas" |

### 4.8 Historias de Usuario (User Stories)

**Formato Estándar**:
```
Como [rol]
Quiero [funcionalidad]
Para [beneficio/valor]
```

**Ejemplos ReMedical**:
```
Historia 1:
Como médico endocrinólogo
Quiero recibir alertas automáticas cuando un paciente tenga riesgo alto de hipoglucemia
Para poder intervenir proactivamente y prevenir emergencias

Criterios de Aceptación:
- Alerta se envía cuando glucosa predicha < 70 mg/dL
- Notificación por email y app móvil
- Incluye recomendaciones de acción inmediata
- Historial de alertas accesible en dashboard

Historia 2:
Como investigador farmacéutico
Quiero simular interacciones de compuestos químicos con proteínas objetivo
Para identificar candidatos prometedores para desarrollo de medicamentos

Criterios de Aceptación:
- Soporte para formatos PDB y MOL2
- Visualización 3D de interacciones moleculares
- Cálculo de afinidad de unión (scoring)
- Exportación de resultados en formato CSV
```

### 4.9 Casos de Uso

**Descripción**: Narrativas detalladas de interacciones sistema-usuario.

**Ejemplo Completo**:
```
Caso de Uso: CU-001 - Predicción de Riesgo de Diabetes

Actor Principal: Médico de Atención Primaria
Objetivo: Evaluar riesgo de diabetes tipo 2 de un paciente
Precondiciones: 
- Médico autenticado en el sistema
- Paciente tiene registro en EHR

Flujo Normal:
1. Médico busca paciente por nombre o ID
2. Sistema muestra ficha del paciente
3. Médico selecciona "Calcular Riesgo Diabetes"
4. Sistema recopila datos: edad, IMC, historial familiar, glucosa en ayunas, HbA1c
5. Sistema ejecuta modelo de ML (XGBoost)
6. Sistema muestra: Riesgo (%), factores contribuyentes, recomendaciones
7. Médico revisa resultados
8. Médico guarda evaluación en historial

Flujos Alternativos:
4a. Faltan datos requeridos
    4a.1 Sistema muestra mensaje "Complete datos faltantes: [lista]"
    4a.2 Médico ingresa datos manualmente o cancela
    
6a. Error en modelo de ML
    6a.1 Sistema muestra "Error temporal, intente nuevamente"
    6a.2 Sistema registra error en logs para análisis

Postcondiciones:
- Evaluación guardada en historial del paciente
- Registro de auditoría creado
- Si riesgo >70%, alerta automática generada

Requisitos No Funcionales:
- Tiempo de respuesta < 3 segundos
- Disponibilidad 99.9%
- Datos encriptados en tránsito y reposo
```

## 5. Matriz de Trazabilidad de Requisitos

Conecta requisitos con casos de prueba, diseño e implementación.

| Req ID | Descripción | Prioridad | Caso de Uso | Módulo | Test Cases | Estado |
|--------|-------------|-----------|-------------|--------|------------|--------|
| REQ-001 | Predicción diabetes ML | Alta | CU-001 | ml_prediction | TC-001, TC-002 | Implementado |
| REQ-002 | Dashboard médicos | Alta | CU-002 | frontend_dash | TC-010-015 | En Desarrollo |
| REQ-003 | Integración EHR | Media | CU-003 | ehr_integration | TC-020-025 | Planeado |

## Referencias

- IEEE Std 830-1998: Recommended Practice for Software Requirements Specifications
- BABOK (Business Analysis Body of Knowledge) v3
- Sommerville, I. (2015). Software Engineering (10th ed.)
- Robertson, S., & Robertson, J. (2012). Mastering the Requirements Process
