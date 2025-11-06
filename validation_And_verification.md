# Validación y Verificación (V&V) de Requisitos - ReMedical

## 1. Conceptos Fundamentales de V&V

### 1.1 Definiciones

**Verificación**: "Are we building the product right?"
- ¿El sistema cumple con las especificaciones y requisitos definidos?
- Enfoque: Corrección técnica, conformidad con estándares
- Pregunta clave: ¿Implementamos correctamente lo que documentamos?

**Validación**: "Are we building the right product?"
- ¿El sistema satisface las necesidades reales del usuario?
- Enfoque: Utilidad, usabilidad, valor de negocio
- Pregunta clave: ¿Estamos construyendo lo que el usuario realmente necesita?

### 1.2 Diferencias Clave

| Aspecto | Verificación | Validación |
|---------|--------------|------------|
| **Momento** | Durante el desarrollo | Al final del desarrollo |
| **Pregunta** | ¿Está bien construido? | ¿Es lo correcto? |
| **Métodos** | Revisiones, inspecciones, testing | Pruebas de usuario, demos, prototipos |
| **Evaluadores** | Equipo técnico, QA | Usuarios finales, stakeholders |
| **Objetivo** | Conformidad con specs | Satisfacción de necesidades |
| **Documentación** | Requisitos técnicos, diseño | Casos de uso, historias de usuario |

### 1.3 Modelo V (V-Model)

```
REQUISITOS                                              VALIDACIÓN
────────────────────────────────────────────────────────────────────
                                                                    
Requisitos de Negocio ─────────────────────────────▶ Acceptance Testing
        │                                                    ▲
        │                                                    │
        ▼                                                    │
Requisitos de Usuario ─────────────────────────────▶ System Testing
        │                                                    ▲
        │                                                    │
        ▼                                                    │
Requisitos Funcionales ────────────────────────────▶ Integration Testing
        │                                                    ▲
        │                                                    │
        ▼                                                    │
Diseño Detallado ──────────────────────────────────▶ Unit Testing
        │                                                    ▲
        │                                                    │
        ▼                                                    │
    IMPLEMENTACIÓN ──────────────────────────────────────────┘
                        (Codificación)

────────────────────────────────────────────────────────────────────
VERIFICACIÓN                                          VALIDACIÓN
```

---

## 2. Técnicas de Verificación de Requisitos

### 2.1 Revisiones de Requisitos (Requirements Reviews)

#### Checklist de Verificación para ReMedical

```
REQUISITO: REMED-R001 - Sistema de Predicción de Diabetes

✅ CRITERIOS DE CALIDAD

COMPLETO:
☐ ¿Especifica todas las entradas necesarias?
   ✓ Sí: edad, IMC, glucosa, HbA1c, historial familiar
☐ ¿Define claramente las salidas esperadas?
   ✓ Sí: porcentaje de riesgo (0-100%), factores contribuyentes
☐ ¿Incluye manejo de excepciones?
   ✓ Sí: manejo de datos faltantes, errores de modelo

CORRECTO:
☐ ¿Es técnicamente factible?
   ✓ Sí: tecnología ML madura (XGBoost), datasets disponibles
☐ ¿Está libre de contradicciones?
   ✓ Revisar: Conflicto con REQ-R005 sobre privacidad de datos
☐ ¿Los stakeholders están de acuerdo?
   ✓ Aprobado por Dr. González (Endocrinología) el 2025-10-15

CONSISTENTE:
☐ ¿Es consistente con otros requisitos?
   ✓ Alineado con REQ-R010 (Integración EHR)
   ⚠ Verificar compatibilidad con REQ-R015 (Cumplimiento HIPAA)
☐ ¿Usa terminología estándar?
   ✓ Términos médicos según SNOMED CT

NO AMBIGUO:
☐ ¿Tiene una sola interpretación posible?
   ⚠ "Predicción rápida" → Redefinir como "<3 segundos"
☐ ¿Los cuantificadores están claros?
   ✓ Sí: "precisión >90%", "recall >85%"

VERIFICABLE:
☐ ¿Se puede testear objetivamente?
   ✓ Sí: métricas cuantitativas (accuracy, F1-score)
☐ ¿Existen criterios de aceptación claros?
   ✓ Sí: 5 criterios definidos en historia de usuario

TRAZABLE:
☐ ¿Está vinculado a necesidad de negocio?
   ✓ Sí: Objetivo "Reducir incidencia diabetes en 20%"
☐ ¿Tiene ID único y versionado?
   ✓ Sí: REMED-R001 v2.1

PRIORIZADO:
☐ ¿Tiene prioridad asignada?
   ✓ Sí: ALTA (MoSCoW: Must Have)
☐ ¿La prioridad está justificada?
   ✓ Sí: Core feature del MVP

REGULATORIO (Específico ReMedical):
☐ ¿Cumple con normativas FDA?
   ✓ Clasificado como FDA Class II (medical device software)
☐ ¿Cumple con HIPAA?
   ✓ Datos encriptados, logs de auditoría, consentimiento informado
☐ ¿Requiere aprobación ética?
   ⚠ Pendiente: Revisión por comité de ética institucional
```

### 2.2 Inspección Formal (Fagan Inspection)

**Proceso de 6 Pasos**:

```
1. PLANIFICACIÓN
   Moderador: Carlos Ramírez (Arquitecto)
   Autor: Ana López (Product Owner)
   Revisores: Juan (Dev), María (Médico), Roberto (QA), Patricia (Legal)
   Material: Documento de Especificación de Requisitos (SRS) v3.0
   Duración estimada: 2 horas

2. VISIÓN GENERAL
   - Ana presenta contexto del sistema de predicción
   - Explica objetivos y alcance
   - Responde preguntas generales
   Duración: 30 minutos

3. PREPARACIÓN INDIVIDUAL
   Cada revisor analiza SRS independientemente
   ┌────────────────────────────────────────────────┐
   │ Juan (Developer):                              │
   │ - Detecta 3 ambigüedades en requisitos de API │
   │ - Identifica falta de spec de rate limiting    │
   │                                                │
   │ María (Médica):                                │
   │ - Señala terminología médica incorrecta        │
   │ - Sugiere agregar validación clínica          │
   │                                                │
   │ Roberto (QA):                                  │
   │ - Encuentra 5 requisitos no testeables        │
   │ - Propone criterios de aceptación específicos │
   └────────────────────────────────────────────────┘
   Duración: 1 hora (cada quien)

4. REUNIÓN DE INSPECCIÓN
   Moderador guía revisión línea por línea
   
   Hallazgos registrados:
   ┌────────────────────────────────────────────────┐
   │ ID: DEF-001                                    │
   │ Tipo: Ambigüedad                               │
   │ Severidad: Alta                                │
   │ Requisito: REMED-R001                          │
   │ Descripción: "Predicción rápida" no está      │
   │              cuantificado                      │
   │ Sugerencia: Definir como "<3 segundos P95"    │
   │ Asignado a: Ana López                          │
   ├────────────────────────────────────────────────┤
   │ ID: DEF-002                                    │
   │ Tipo: Omisión                                  │
   │ Severidad: Media                               │
   │ Requisito: REMED-R002                          │
   │ Descripción: Falta especificar qué hacer con  │
   │              pacientes <18 años                │
   │ Sugerencia: Agregar restricción de edad       │
   │ Asignado a: Ana López                          │
   └────────────────────────────────────────────────┘
   
   Métricas:
   - Total defectos: 12
   - Críticos: 2, Altos: 4, Medios: 5, Bajos: 1
   - Densidad: 12 defectos / 45 requisitos = 0.27 defectos/req

   Duración: 2 horas

5. CORRECCIÓN
   Ana López corrige defectos identificados
   - Reescribe 8 requisitos
   - Agrega 3 requisitos nuevos (casos edge)
   - Elimina 1 requisito duplicado
   Duración: 1 día

6. SEGUIMIENTO
   Moderador verifica que todas las correcciones se implementaron
   Decisión: ✅ APROBADO para pasar a diseño
   Duración: 30 minutos
```

**Métricas de Efectividad**:
```
Costo de Inspección:
- 6 personas × 4 horas = 24 horas-persona
- @ $50/hora = $1,200

Defectos encontrados: 12

Costo por defecto: $1,200 / 12 = $100

Ahorro estimado:
- Corregir en fase de requisitos: $100/defecto
- Corregir en producción: $10,000/defecto
- ROI = ($10,000 - $100) × 12 = $118,800 ahorrados
```

### 2.3 Verificación Automatizada con Herramientas

#### Análisis de Lenguaje Natural (NLP)

**Herramienta**: [IBM DOORS](https://www.ibm.com/products/requirements-management), [Jama Connect](https://www.jamasoftware.com/)

**Ejemplo de Detección Automática**:

```
REQUISITO ORIGINAL:
"El sistema debe predecir rápidamente el riesgo de diabetes de todos los 
pacientes usando algoritmos inteligentes y mostrar resultados bonitos."

🚨 PROBLEMAS DETECTADOS:

1. Término vago: "rápidamente"
   Sugerencia: Especificar "<3 segundos"

2. Término vago: "todos los pacientes"
   ¿Incluye menores de edad? ¿Pacientes embarazadas?
   Sugerencia: "pacientes adultos (18-75 años) sin diabetes diagnosticada"

3. Término subjetivo: "bonitos"
   Sugerencia: "en dashboard con código de colores (verde/amarillo/rojo)"

4. Término vago: "algoritmos inteligentes"
   Sugerencia: "modelo XGBoost entrenado con dataset de 50K pacientes"

5. Lenguaje pasivo: "debe predecir"
   Sugerencia: "El sistema predice..." (voz activa)

6. Falta cuantificación: Sin métricas de precisión
   Sugerencia: Agregar "con accuracy >90% y recall >85%"

REQUISITO MEJORADO:
"El sistema predice el riesgo de diabetes tipo 2 en pacientes adultos 
(18-75 años) sin diabetes diagnosticada previa, utilizando un modelo 
XGBoost entrenado con 50,000 registros clínicos. La predicción se completa 
en menos de 3 segundos (percentil 95) y se muestra en un dashboard con 
código de colores (verde: 0-30%, amarillo: 31-60%, rojo: 61-100%). 
El modelo alcanza un accuracy >90% y recall >85% en el conjunto de 
validación."
```

### 2.4 Verificación de Requisitos No Funcionales (ISO/IEC 25010)

**Categorías según ISO/IEC 25010 (SQuaRE)**:

#### Ejemplo 1: Requisito de Desempeño

```
REQUISITO: REMED-NFR-001
Categoría: Eficiencia de Desempeño → Tiempo de Respuesta
Descripción: El sistema debe calcular la predicción de diabetes en <3 segundos

VERIFICACIÓN:
✅ Método: Performance testing con JMeter
✅ Escenario:
   - Carga: 100 usuarios concurrentes
   - Dataset: 1,000 pacientes con datos completos
   - Infraestructura: AWS EC2 m5.large
✅ Criterio de Aceptación:
   - P50 (mediana): <2 segundos
   - P95 (percentil 95): <3 segundos
   - P99 (percentil 99): <5 segundos
✅ Resultado del Test:
   - P50: 1.8 seg ✓
   - P95: 2.7 seg ✓
   - P99: 4.2 seg ✓
   
ESTADO: ✅ VERIFICADO
```

#### Ejemplo 2: Requisito de Seguridad

```
REQUISITO: REMED-NFR-010
Categoría: Seguridad → Confidencialidad
Descripción: Los datos de pacientes (PHI) deben estar encriptados en 
             tránsito y en reposo

VERIFICACIÓN:
✅ Método: Auditoría de seguridad + Penetration testing
✅ Checklist:
   ☐ Encriptación en tránsito:
      ✓ HTTPS con TLS 1.3
      ✓ Certificados SSL válidos (Let's Encrypt)
      ✓ Perfect Forward Secrecy habilitado
      
   ☐ Encriptación en reposo:
      ✓ Base de datos PostgreSQL con Transparent Data Encryption (TDE)
      ✓ S3 buckets con SSE-S3 (Server-Side Encryption)
      ✓ Secrets en AWS Secrets Manager (encriptados con KMS)
      
   ☐ Gestión de claves:
      ✓ Claves rotadas cada 90 días
      ✓ Claves de backup en vault separado
      
   ☐ Auditoría:
      ✓ Logs de acceso a datos cifrados
      ✓ Alertas de accesos anómalos configuradas

✅ Penetration Test:
   - Herramienta: OWASP ZAP
   - Vulnerabilidades encontradas: 0 críticas, 2 bajas
   - Reporte: pentest_report_2025-11-01.pdf

ESTADO: ✅ VERIFICADO
```

#### Ejemplo 3: Requisito de Usabilidad

```
REQUISITO: REMED-NFR-015
Categoría: Usabilidad → Facilidad de Aprendizaje
Descripción: Un médico sin experiencia previa debe poder generar su primera 
             predicción en <10 minutos sin ayuda externa

VERIFICACIÓN:
✅ Método: Usability Testing con usuarios reales
✅ Participantes:
   - 5 médicos endocrinólogos (sin exposición previa al sistema)
   - Edades: 28-52 años
   - Experiencia con software médico: Básica a Avanzada

✅ Protocolo:
   1. Dar acceso al sistema (usuario/contraseña)
   2. Tarea: "Calcule la predicción de riesgo de diabetes para el paciente 
      Juan Pérez (ID: 12345)"
   3. Medir tiempo hasta completar tarea
   4. No intervenir salvo que abandonen (>15 min)

✅ Resultados:
   Médico A: 6 min 23 seg ✓
   Médico B: 8 min 01 seg ✓
   Médico C: 9 min 47 seg ✓
   Médico D: 11 min 12 seg ✗ (excede 10 min)
   Médico E: 7 min 55 seg ✓
   
   Promedio: 8 min 38 seg
   Tasa de éxito: 80% (4/5 dentro de límite)

✅ Feedback cualitativo:
   - Positivo: "UI intuitivo", "Colores claros"
   - Negativo: "No encontré botón de búsqueda rápido" (Médico D)

ACCIONES CORRECTIVAS:
- Agregar búsqueda de paciente con shortcut Ctrl+F
- Añadir tooltip en botón "Calcular predicción"
- Re-test programado para 2025-11-15

ESTADO: ⚠️ PARCIALMENTE VERIFICADO (80% éxito, objetivo >90%)
```

---

## 3. Técnicas de Validación de Requisitos

### 3.1 Prototipado Rápido

#### Ejemplo: Dashboard de Predicción IA

```
FASE 1: Prototipo de Baja Fidelidad (Wireframe en papel)
┌────────────────────────────────────────────────────────┐
│ ReMedical - Predicción de Diabetes      [@usuario ▼] │
├────────────────────────────────────────────────────────┤
│                                                        │
│ [🔍 Buscar paciente...]                   [+ Nuevo]   │
│                                                        │
│ ┌──────────────────┬─────────────────────────────────┐│
│ │ Lista Pacientes  │  PREDICCIÓN DE RIESGO           ││
│ │ (150 total)      │                                 ││
│ │                  │  Juan Pérez (45 años)           ││
│ │ ☐ Juan Pérez     │  ID: 12345                      ││
│ │ ☐ Ana García     │                                 ││
│ │ ☐ Pedro López    │  ┌─────────────────────┐        ││
│ │ ☐ ...            │  │   RIESGO: 72%       │        ││
│ │                  │  │   [████████░░] ALTO │        ││
│ │                  │  └─────────────────────┘        ││
│ │                  │                                 ││
│ │                  │  Factores:                      ││
│ │                  │  • IMC elevado: 35%             ││
│ │                  │  • Glucosa alta: 28%            ││
│ │                  │  • Edad: 22%                    ││
│ │                  │                                 ││
│ │                  │  [📊 Ver Historial]             ││
│ │                  │  [📄 Exportar PDF]              ││
│ └──────────────────┴─────────────────────────────────┘│
└────────────────────────────────────────────────────────┘

VALIDACIÓN:
✅ Sesión con 3 médicos (30 min cada uno)
✅ Feedback:
   - Dr. González: "Me gusta el código de colores, muy claro"
   - Dr. Martínez: "Necesito ver valores de laboratorio también"
   - Dra. Rodríguez: "¿Puedo comparar con predicciones anteriores?"
   
ITERACIÓN: Agregar sección "Valores de laboratorio" y gráfico de tendencia

──────────────────────────────────────────────────────────

FASE 2: Prototipo de Alta Fidelidad (Figma interactivo)
🔗 https://figma.com/remedial-dashboard-v2

VALIDACIÓN:
✅ Usability testing con 5 médicos
✅ Tareas:
   1. Encontrar paciente "María López"
   2. Calcular predicción de riesgo
   3. Interpretar resultado
   4. Exportar reporte

✅ Métricas:
   - Tasa de éxito: 100% (5/5 completaron todas las tareas)
   - Tiempo promedio: 4 min 12 seg
   - SUS Score (System Usability Scale): 82/100 (Excelente)

✅ Citas de médicos:
   "Esto realmente ahorraría tiempo en mi consulta diaria" - Dr. Martínez
   "La visualización de factores es muy útil para explicar al paciente" - Dra. Rodríguez

DECISIÓN: ✅ VALIDADO - Proceder a implementación

──────────────────────────────────────────────────────────

FASE 3: MVP Funcional (React + Backend)

VALIDACIÓN:
✅ Pilot con 10 médicos en 2 hospitales (30 días)
✅ Métricas reales:
   - 324 predicciones realizadas
   - Tiempo promedio por predicción: 2.3 segundos ✓
   - Satisfacción: 8.5/10
   - Reportes de bugs: 3 (todos severidad baja)

✅ Casos de uso reales:
   "Detectamos a un paciente con riesgo 89% que no estaba en nuestro 
    radar. Iniciamos intervención preventiva a tiempo." 
    - Dra. González, Hospital General

DECISIÓN: ✅ VALIDADO - Lanzar a producción
```

### 3.2 Pruebas de Aceptación de Usuario (UAT)

#### Escenario Completo: Sistema de Predicción

```
PLAN DE UAT - ReMedical Predicción de Diabetes
Fecha: 2025-11-10 al 2025-11-17 (1 semana)
Participantes: 8 médicos endocrinólogos de 3 hospitales

┌─────────────────────────────────────────────────────────────┐
│ CASO DE PRUEBA UAT-001: Predicción Básica                  │
├─────────────────────────────────────────────────────────────┤
│ Objetivo: Validar flujo completo de predicción             │
│                                                             │
│ Precondiciones:                                             │
│ - Usuario autenticado como médico                          │
│ - Base de datos con 100 pacientes de prueba                │
│                                                             │
│ Pasos:                                                      │
│ 1. Buscar paciente "Carlos Hernández" (ID: 67890)          │
│ 2. Click en "Calcular Riesgo de Diabetes"                  │
│ 3. Revisar resultado mostrado                              │
│ 4. Click en "Ver Factores Contribuyentes"                  │
│ 5. Click en "Exportar PDF"                                 │
│                                                             │
│ Resultados Esperados:                                       │
│ ✓ Paciente encontrado en <2 segundos                       │
│ ✓ Predicción calculada en <3 segundos                      │
│ ✓ Resultado muestra: porcentaje, código color, clasificación│
│ ✓ Factores listados con pesos (suma 100%)                  │
│ ✓ PDF descargado con toda la información                   │
│                                                             │
│ Resultados Reales (Dr. González):                          │
│ ✓ Búsqueda: 1.2 seg                                        │
│ ✓ Predicción: 2.8 seg                                      │
│ ✓ Riesgo: 68% (Moderado-Alto, amarillo)                    │
│ ✓ Factores: IMC 32%, Glucosa 28%, Edad 20%, Otro 20%      │
│ ✓ PDF generado correctamente                               │
│                                                             │
│ Comentarios:                                                │
│ "Sistema rápido y fácil de usar. El PDF es muy profesional │
│  para mostrar al paciente."                                │
│                                                             │
│ ESTADO: ✅ APROBADO                                          │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ CASO DE PRUEBA UAT-002: Manejo de Datos Incompletos        │
├─────────────────────────────────────────────────────────────┤
│ Objetivo: Validar que el sistema maneja correctamente      │
│           pacientes con información faltante               │
│                                                             │
│ Pasos:                                                      │
│ 1. Buscar paciente "Ana Ramírez" (sin valor de HbA1c)      │
│ 2. Intentar calcular predicción                            │
│                                                             │
│ Resultados Esperados:                                       │
│ ✓ Sistema muestra mensaje: "Faltan datos requeridos:       │
│   HbA1c. ¿Desea ingresar manualmente?"                     │
│ ✓ Ofrece formulario para completar                         │
│ ✓ Muestra campos obligatorios vs opcionales                │
│                                                             │
│ Resultados Reales (Dra. Martínez):                         │
│ ✗ Error: Sistema mostró error técnico en lugar de mensaje  │
│    amigable: "NaN value in feature vector"                 │
│                                                             │
│ BUG REPORTADO: REMED-BUG-045                                │
│ Severidad: Alta                                             │
│ Asignado a: Ana López (Backend)                            │
│                                                             │
│ ESTADO: ❌ RECHAZADO (requiere corrección)                  │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ CASO DE PRUEBA UAT-003: Validación Clínica                 │
├─────────────────────────────────────────────────────────────┤
│ Objetivo: Validar que las predicciones son clínicamente    │
│           coherentes con juicio médico experto             │
│                                                             │
│ Método: Panel de 3 endocrinólogos revisan 20 casos         │
│         y comparan predicción del sistema vs su evaluación │
│                                                             │
│ Resultados:                                                 │
│                                                             │
│ Concordancia Sistema-Médicos:                               │
│ - Casos de bajo riesgo: 18/20 (90%)                        │
│ - Casos de alto riesgo: 19/20 (95%)                        │
│ - Casos moderados: 14/20 (70%)                             │
│                                                             │
│ Discrepancias notables:                                     │
│ Caso #7: Sistema 58% (Moderado), Médicos 75% (Alto)        │
│ Razón: Sistema no consideró antecedente de diabetes        │
│        gestacional (no estaba en features del modelo)      │
│                                                             │
│ Caso #12: Sistema 82% (Alto), Médicos 60% (Moderado)       │
│ Razón: Paciente tiene IMC alto pero es atleta              │
│        (sistema no diferencia masa muscular vs grasa)      │
│                                                             │
│ ACCIONES:                                                   │
│ 1. Agregar "diabetes gestacional previa" como feature      │
│ 2. Investigar incorporar composición corporal              │
│ 3. Re-entrenar modelo con estos features                   │
│                                                             │
│ ESTADO: ⚠️ APROBADO CON RESERVAS                            │
│         (aprobar para producción, planear mejoras v2)      │
└─────────────────────────────────────────────────────────────┘

RESUMEN UAT:
┌────────────────────────────────────────────┐
│ Total casos de prueba: 15                  │
│ Aprobados: 12 (80%)                        │
│ Rechazados: 2 (13%)                        │
│ Aprobados con reservas: 1 (7%)             │
│                                            │
│ Bugs encontrados: 5                        │
│ - Críticos: 0                              │
│ - Altos: 2 (bloqueantes)                   │
│ - Medios: 2                                │
│ - Bajos: 1                                 │
│                                            │
│ Satisfacción de usuarios: 8.2/10           │
│                                            │
│ DECISIÓN: RETRASAR LANZAMIENTO 1 SEMANA    │
│           para corregir bugs de alta       │
│           severidad                        │
└────────────────────────────────────────────┘
```

### 3.3 Validación con Stakeholders (Sprint Review)

```
SPRINT 5 REVIEW - ReMedical
Fecha: 2025-11-05 14:00-16:00
Asistentes:
- Product Owner: Ana López
- Scrum Master: Carlos Ramírez
- Equipo Dev: Juan, Laura, Patricia (5 personas)
- Stakeholders:
  * Dr. María González (Médica líder)
  * Ing. Roberto Sánchez (CTO)
  * Lic. Carmen Díaz (Asuntos Regulatorios)
  * Inversores: 2 representantes

AGENDA:
──────────────────────────────────────────────────────────

[14:00-14:10] Bienvenida y objetivos del sprint
Ana (PO): "En Sprint 5 nos comprometimos a 34 Story Points,
completamos 32 SP (94%). Las 2 SP restantes se movieron a Sprint 6."

[14:10-14:40] DEMO: Dashboard de Predicción de Diabetes (REMED-101)
Juan (Dev): [Pantalla compartida]

1. Login en sistema
2. Búsqueda de paciente "Juan Pérez"
3. Click "Calcular Riesgo"
   → Resultado: 72% Alto Riesgo (en 2.5 seg) ✓
4. Visualización de factores contribuyentes
   → Gráfico de barras interactivo ✓
5. Exportación a PDF
   → Descarga en 1.8 seg ✓

Dr. González: "Impresionante! Esto es justo lo que necesitamos. 
               Una pregunta: ¿Puedo ver el historial de predicciones?"

Juan: "Aún no, eso está planificado para Sprint 6 (REMED-105)"

Dr. González: "Perfecto, lo esperamos con ansias"

[14:40-15:00] DEMO: Modelo ML de Predicción (REMED-102)
Laura (ML Engineer): [Jupyter Notebook compartido]

Métricas del modelo XGBoost:
- Accuracy: 91.3% ✓ (objetivo >90%)
- Precision: 89.7%
- Recall: 88.2% ✓ (objetivo >85%)
- F1-Score: 88.9%
- AUC-ROC: 0.94 ✓

Curva ROC mostrada...

Ing. Sánchez (CTO): "¿Cómo manejamos el overfitting?"

Laura: "Usamos validación cruzada 10-fold y regularización L2. 
        El modelo generaliza bien en el test set."

[15:00-15:20] DEMO: Integración con EHR (REMED-103)
Patricia (Backend): [Postman collection compartida]

Demostración de API:
1. Autenticación OAuth 2.0 con Epic EHR ✓
2. Query de datos de paciente vía FHIR ✓
3. Transformación a formato interno ✓
4. Manejo de errores (timeout, datos faltantes) ✓

Lic. Díaz (Regulatorio): "¿Cumple con HIPAA?"

Patricia: "Sí, todos los datos se transmiten por HTTPS con TLS 1.3,
           y generamos logs de auditoría para cada acceso."

Lic. Díaz: "Excelente, necesitaré ver esos logs para el reporte FDA"

[15:20-15:40] Feedback y Validación

VOTACIÓN: ¿Aceptan el trabajo completado?
✅ Dr. González: SÍ (con solicitud de historial en v2)
✅ Ing. Sánchez: SÍ
✅ Lic. Díaz: SÍ (pendiente revisión de documentación compliance)
✅ Inversores: SÍ (impresionados con progreso)

Ana (PO): "Todas las historias del sprint son ACEPTADAS"

[15:40-16:00] Planificación de Sprint 6

Prioridades:
1. Corregir 2 bugs de UAT (ALTA prioridad)
2. Agregar historial de predicciones (REMED-105)
3. Mejorar performance para >1000 pacientes (REMED-106)

Dr. González: "¿Cuándo podemos hacer piloto en el hospital?"

Ana (PO): "Si Sprint 6 y 7 van bien, estimamos piloto para diciembre"

FIN DE SESIÓN - Equipo satisfecho, stakeholders emocionados ✅
```

---

## 4. Validación y Verificación en ReMedical

### 4.1 Checklist Específico de ReMedical

```
REQUISITO: Sistema de Predicción de Diabetes con IA

✅ VERIFICACIÓN (Correcto técnicamente)

☐ Conformidad con Especificaciones:
   ✓ Algoritmo ML: XGBoost (según SRS v3.0)
   ✓ Tiempo respuesta: <3 seg P95 (medido: 2.7 seg)
   ✓ Precisión: >90% (logrado: 91.3%)

☐ Cumplimiento Regulatorio:
   ✓ FDA 21 CFR Part 11: Audit trails implementados
   ✓ HIPAA: Encriptación end-to-end
   ✓ ISO 13485: Documentación de gestión de calidad

☐ Estándares de Codificación:
   ✓ PEP 8 (Python style guide)
   ✓ Code coverage >80% (actual: 87%)
   ✓ Zero critical security vulnerabilities (SonarQube)

☐ Interoperabilidad:
   ✓ Integración FHIR con Epic EHR
   ✓ API REST con OpenAPI spec
   ✓ Formato de datos: JSON, CSV, HL7

──────────────────────────────────────────────────────────

✅ VALIDACIÓN (Valor para el usuario)

☐ Validación Clínica:
   ✓ Panel de médicos: 3 endocrinólogos revisaron
   ✓ Concordancia con juicio clínico: 85%
   ✓ Publicación científica: Paper en revisión (JMIR)

☐ Usabilidad:
   ✓ SUS Score: 82/100 (Excelente)
   ✓ Tiempo de aprendizaje: <10 min
   ✓ Satisfacción médicos: 8.5/10

☐ Impacto en Workflow:
   ✓ Tiempo ahorrado: 15 min/paciente
   ✓ Pacientes de alto riesgo detectados: +23%
   ✓ Adopción: 68% de médicos en piloto

☐ Retorno de Inversión (ROI):
   ✓ Costo desarrollo: $250K
   ✓ Ingreso proyectado año 1: $1.2M
   ✓ ROI: 380%

☐ Validación Ética:
   ✓ Consentimiento informado implementado
   ✓ Equidad: Modelo validado en diferentes etnias
   ✓ Transparencia: Explicabilidad de factores (SHAP)
```

### 4.2 Matriz de Trazabilidad Requisitos-Tests

```
┌───────────────────────────────────────────────────────────────────┐
│ MATRIZ DE TRAZABILIDAD - ReMedical Predicción Diabetes           │
├───────────┬────────────────┬──────────────────┬──────────────────┤
│ Requisito │ Historia Usuario│ Tests Unitarios  │ Tests UAT        │
├───────────┼────────────────┼──────────────────┼──────────────────┤
│ REMED-R001│ REMED-101      │ TC-U-001 ✓       │ UAT-001 ✓        │
│ Predicción│ Dashboard UI   │ TC-U-002 ✓       │ UAT-002 ✗        │
│ <3 seg    │                │ TC-U-003 ✓       │ UAT-003 ⚠        │
│           │                │ Cobertura: 92%   │ Éxito: 80%       │
├───────────┼────────────────┼──────────────────┼──────────────────┤
│ REMED-R002│ REMED-102      │ TC-U-010 ✓       │ UAT-010 ✓        │
│ Modelo ML │ Modelo XGBoost │ TC-U-011 ✓       │ UAT-011 ✓        │
│ Acc >90%  │                │ TC-U-012 ✓       │ Validación       │
│           │                │ TC-U-013 ✓       │ médica: ✓        │
│           │                │ Cobertura: 88%   │                  │
├───────────┼────────────────┼──────────────────┼──────────────────┤
│ REMED-R003│ REMED-103      │ TC-U-020 ✓       │ UAT-020 ✓        │
│ Integración│ Integración   │ TC-U-021 ✓       │ UAT-021 ✓        │
│ EHR (FHIR)│ EHR            │ TC-U-022 ⚠       │ Piloto hospital: │
│           │                │ Cobertura: 75%   │ En progreso      │
└───────────┴────────────────┴──────────────────┴──────────────────┘

LEYENDA:
✓ = Pasado
✗ = Fallido
⚠ = Pendiente/En progreso

COBERTURA TOTAL:
- Requisitos con tests: 100% (3/3)
- Requisitos verificados: 100% (3/3)
- Requisitos validados: 67% (2/3) - REMED-R003 en piloto
```

---

## 5. Herramientas para V&V

| Categoría | Herramienta | Uso en ReMedical |
|-----------|-------------|------------------|
| **Gestión de Requisitos** | Jira | Tracking de historias de usuario |
| | Confluence | Documentación de especificaciones |
| | IBM DOORS | Gestión de requisitos regulatorios FDA |
| **Testing Funcional** | Pytest | Tests unitarios (Python backend) |
| | Jest | Tests unitarios (React frontend) |
| | Selenium | Tests E2E de UI |
| | Postman | Tests de API REST |
| **Testing No Funcional** | JMeter | Performance testing |
| | OWASP ZAP | Security testing |
| | Lighthouse | Usability y accessibility |
| **Análisis Estático** | SonarQube | Calidad de código, vulnerabilidades |
| | ESLint | Linting JavaScript/TypeScript |
| | Black | Formateo Python |
| **Validación Médica** | Jupyter Notebook | Análisis de métricas de modelo ML |
| | SHAP | Explicabilidad de predicciones |
| | Tableau | Dashboards para stakeholders médicos |
| **Cumplimiento** | Veracode | Análisis de seguridad (FDA requerido) |
| | GitHub Actions | CI/CD con validaciones automáticas |

---

## 6. Mejores Prácticas

### ✅ DOs

1. **V&V desde el Día 1**
   - No esperar al final del proyecto
   - Revisiones de requisitos antes de codificar

2. **Involucrar a Usuarios Reales**
   - Médicos reales en UAT, no solo QA
   - Observar uso en contexto real (hospitales)

3. **Automatizar lo Repetible**
   - Tests unitarios automáticos en CI/CD
   - Checks de calidad de requisitos (NLP tools)

4. **Documentar Decisiones**
   - Por qué se aceptó/rechazó un requisito
   - Rationale de decisiones de diseño (ADRs)

5. **Metr ir, Medir, Medir**
   - Métricas de V&V (defect density, test coverage)
   - Tracking de efectividad (bugs en prod después de V&V)

### ❌ DON'Ts

1. **No confundir V&V**
   - Verificación ≠ Validación
   - Ambas son necesarias

2. **No hacer V&V solo al final**
   - "Waterfall trap": dejar testing para el final
   - V&V iterativo en cada sprint

3. **No ignorar requisitos no funcionales**
   - Performance, seguridad, usabilidad son críticos
   - Especialmente en healthcare (regulaciones)

4. **No hacer V&V sin trazabilidad**
   - Cada requisito debe tener tests asociados
   - Matriz de trazabilidad obligatoria

5. **No omitir validación clínica**
   - En healthcare, validación médica es mandatoria
   - Panel de expertos debe revisar

---

## Referencias

- IEEE Std 829-2008: Standard for Software and System Test Documentation
- IEEE Std 1012-2016: Standard for System, Software, and Hardware Verification and Validation
- ISO/IEC 25010:2011: Systems and software Quality Requirements and Evaluation (SQuaRE)
- FDA. (2023). Software as a Medical Device (SaMD): Clinical Evaluation Guidance
- Sommerville, I. (2015). Software Engineering (10th ed.) - Chapter on V&V


