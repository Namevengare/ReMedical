# Historias de Usuario - ReMedical

---

## Formato

**Como** [rol] **Quiero** [funcionalidad] **Para** [beneficio]

Cada historia incluye: ID, Prioridad (MoSCoW), Story Points, Criterios de Aceptación, Dependencias.

---



## Epic 1: Gestión de Pacientes

### Historia: Búsqueda de Pacientes

**ID**: REMED-US-001  
**Prioridad**: Must Have  
**Story Points**: 3  
**Sprint**: 1

**Historia**:  
Como médico endocrinólogo  
Quiero buscar pacientes por nombre, apellido o número de historia clínica  
Para acceder rápidamente a su información sin navegar por listas largas

**Criterios de Aceptación**:
1. El campo de búsqueda está visible en la pantalla principal del dashboard
2. La búsqueda funciona con mínimo 3 caracteres ingresados
3. Los resultados se muestran en menos de 2 segundos
4. La búsqueda es case-insensitive
5. Se puede buscar por: nombre completo, apellido, o número de historia clínica (MRN)
6. Los resultados muestran: nombre completo, edad, MRN, última consulta
7. Hacer click en un resultado carga el perfil completo del paciente

**Notas Técnicas**:
- Implementar índice full-text en PostgreSQL
- Considerar fuzzy matching para nombres con typos
- Limitar resultados a 50 primeros, ordenados por relevancia

**Dependencias**: Ninguna

**Mockup**: Ver Figma dashboard-v2-search

---

### Historia: Visualización de Perfil de Paciente

**ID**: REMED-US-002  
**Prioridad**: Must Have  
**Story Points**: 5  
**Sprint**: 1

**Historia**:  
Como médico endocrinólogo  
Quiero ver el perfil completo de un paciente en una sola pantalla  
Para tener contexto completo al momento de evaluar su riesgo de diabetes

**Criterios de Aceptación**:
1. El perfil muestra datos demográficos: nombre, edad, género, altura, peso, IMC
2. Se muestra historial de valores clínicos: glucosa, HbA1c, presión arterial (últimos 12 meses)
3. Se visualiza historial familiar de diabetes (sí/no, relación)
4. Se muestran predicciones previas si existen
5. Toda la información cabe en una pantalla de 1920x1080 sin scroll (excepto historial extenso)
6. Los valores fuera de rango normal están resaltados en color naranja/rojo
7. Hay botón claramente visible para "Calcular Nueva Predicción"

**Notas Técnicas**:
- Integración con EHR para obtener datos clínicos vía HL7 FHIR
- Cachear datos de paciente por 5 minutos para reducir latencia
- Calcular IMC automáticamente si no viene del EHR

**Dependencias**: REMED-US-001 (búsqueda)

---

### Historia: Registro Manual de Datos Clínicos

**ID**: REMED-US-003  
**Prioridad**: Should Have  
**Story Points**: 8  
**Sprint**: 3

**Historia**:  
Como médico endocrinólogo  
Quiero poder ingresar o actualizar datos clínicos manualmente  
Para casos donde el EHR no está disponible o los datos no están sincronizados

**Criterios de Aceptación**:
1. Hay un botón "Editar Datos" en el perfil del paciente
2. Se puede editar: peso, altura, glucosa en ayunas, HbA1c, presión arterial, historial familiar
3. El formulario valida rangos: peso (30-300 kg), altura (100-250 cm), glucosa (50-600 mg/dL), HbA1c (4-18%)
4. Se muestra warning si valor está fuera de rango normal pero se permite guardar
5. Cada cambio queda registrado con timestamp y usuario que lo realizó (auditoría)
6. Los cambios manuales se marcan visualmente como "No sincronizado con EHR"
7. El IMC se recalcula automáticamente al cambiar peso o altura

**Notas Técnicas**:
- Implementar validación en frontend y backend
- Tabla de auditoría separada para compliance HIPAA
- Considerar flag "source: manual | ehr" en cada dato

**Dependencias**: REMED-US-002 (perfil de paciente)

---

## Epic 2: Predicción de Riesgo de Diabetes

### Historia: Cálculo de Predicción de Riesgo

**ID**: REMED-US-010  
**Prioridad**: Must Have  
**Story Points**: 13  
**Sprint**: 4-5

**Historia**:  
Como médico endocrinólogo  
Quiero calcular el riesgo de diabetes tipo 2 de un paciente con un solo click  
Para identificar rápidamente pacientes que requieren intervención preventiva

**Criterios de Aceptación**:
1. Hay un botón prominente "Calcular Riesgo de Diabetes" en el perfil del paciente
2. El sistema valida que existen los datos mínimos requeridos: edad, IMC, glucosa o HbA1c
3. Si faltan datos, se muestra mensaje específico indicando qué datos se necesitan
4. La predicción se completa en menos de 3 segundos (percentil 95)
5. El resultado muestra: porcentaje de riesgo (0-100%), categoría (Bajo/Moderado/Alto), nivel de confianza
6. Se usa código de colores: Verde (0-30%), Amarillo (31-60%), Rojo (61-100%)
7. El resultado se guarda automáticamente en el historial del paciente
8. Se registra en log de auditoría: usuario, timestamp, versión del modelo

**Notas Técnicas**:
- Modelo: XGBoost entrenado con 50,000 registros
- Accuracy objetivo: >90%, Recall >85%
- API asíncrona para no bloquear UI
- Caché de predicciones por 24 horas si datos no cambian

**Dependencias**: REMED-US-002 (perfil de paciente)

**Modelo de ML**: Ver docs/ml_model_specification.md

---

### Historia: Explicabilidad de Predicción

**ID**: REMED-US-011  
**Prioridad**: Must Have  
**Story Points**: 8  
**Sprint**: 6

**Historia**:  
Como médico endocrinólogo  
Quiero entender qué factores contribuyeron más a la predicción de riesgo  
Para poder explicarle al paciente las razones específicas de su riesgo y enfocar intervenciones

**Criterios de Aceptación**:
1. Debajo del score de riesgo, se muestra sección "Factores Contribuyentes"
2. Se listan los top 5 factores que más influenciaron la predicción
3. Cada factor muestra: nombre comprensible, valor del paciente, impacto porcentual
4. Los impactos suman aproximadamente 100%
5. Se usa lenguaje clínico comprensible, no técnico (ej: "IMC elevado" no "feature_bmi")
6. Cada factor tiene tooltip con explicación adicional si se hace hover
7. Hay link a "Ver explicación detallada" que muestra gráfico SHAP values

**Notas Técnicas**:
- Usar SHAP (SHapley Additive exPlanations) para explicabilidad
- Pre-calcular SHAP values al momento de predicción para no agregar latencia
- Mapeo de features técnicos a nombres clínicos en diccionario

**Dependencias**: REMED-US-010 (predicción)

---

### Historia: Historial de Predicciones

**ID**: REMED-US-012  
**Prioridad**: Should Have  
**Story Points**: 5  
**Sprint**: 7

**Historia**:  
Como médico endocrinólogo  
Quiero ver el historial de predicciones previas de un paciente  
Para evaluar cómo ha evolucionado su riesgo a lo largo del tiempo

**Criterios de Aceptación**:
1. En el perfil del paciente hay sección "Historial de Predicciones"
2. Se muestran todas las predicciones ordenadas por fecha (más reciente primero)
3. Cada entrada muestra: fecha, riesgo porcentual, categoría, médico que la solicitó
4. Se puede expandir cada predicción para ver factores contribuyentes de ese momento
5. Hay gráfico de línea mostrando evolución del riesgo en el tiempo
6. Se pueden comparar dos predicciones lado a lado (checkbox para seleccionar)

**Notas Técnicas**:
- Usar Chart.js o D3.js para gráfico de evolución
- Paginación si hay más de 20 predicciones
- Considerar exportación a CSV del historial

**Dependencias**: REMED-US-010 (predicción), REMED-US-011 (explicabilidad)

---

## Epic 3: Reportes y Exportación

### Historia: Exportación de Reporte en PDF

**ID**: REMED-US-020  
**Prioridad**: Must Have  
**Story Points**: 8  
**Sprint**: 8

**Historia**:  
Como médico endocrinólogo  
Quiero exportar el reporte de predicción en formato PDF  
Para compartirlo con el paciente y archivarlo en su expediente físico

**Criterios de Aceptación**:
1. Hay botón "Exportar PDF" visible en la pantalla de predicción
2. El PDF se genera en menos de 5 segundos
3. El PDF incluye: logo del hospital, datos del paciente (anonimizables), fecha, score de riesgo con código de colores, factores contribuyentes, disclaimer legal, firma digital del médico
4. El PDF es profesional, legible, y en formato carta (8.5" x 11")
5. El PDF se puede descargar o enviar por email al paciente (con consentimiento)
6. Se registra en auditoría cada vez que se genera un PDF

**Notas Técnicas**:
- Usar biblioteca: ReportLab (Python) o PDFKit
- Template de PDF customizable por hospital
- Incluir QR code con link a versión digital (si paciente tiene portal)

**Dependencias**: REMED-US-010 (predicción), REMED-US-011 (explicabilidad)

---

### Historia: Dashboard de Población

**ID**: REMED-US-021  
**Prioridad**: Should Have  
**Story Points**: 13  
**Sprint**: 10-11

**Historia**:  
Como administrador de salud poblacional  
Quiero ver estadísticas agregadas de riesgo de diabetes en mi población de pacientes  
Para identificar grupos de alto riesgo y planificar programas de prevención

**Criterios de Aceptación**:
1. Hay vista "Dashboard Poblacional" accesible desde menú principal
2. Se muestran métricas: total de pacientes evaluados, % en cada categoría de riesgo, tendencia mensual
3. Se pueden aplicar filtros: rango de edad, género, hospital
4. Hay gráficos visuales: distribución de riesgo (histograma), evolución temporal (línea), factores de riesgo más comunes (barra)
5. Se puede exportar reporte agregado en Excel o PDF
6. Los datos son anónimos (no se muestran nombres de pacientes)
7. Dashboard se actualiza en tiempo real conforme se agregan predicciones

**Notas Técnicas**:
- Usar PostgreSQL aggregate queries optimizadas
- Cachear resultados por 1 hora para dashboard
- Considerar Tableau o similar para analytics avanzado

**Dependencias**: REMED-US-010 (predicción)

---

## Epic 4: Integración con EHR

### Historia: Sincronización Automática de Datos

**ID**: REMED-US-030  
**Prioridad**: Must Have  
**Story Points**: 21  
**Sprint**: 2-4 (background)

**Historia**:  
Como médico endocrinólogo  
Quiero que los datos clínicos de mis pacientes se sincronicen automáticamente desde el EHR del hospital  
Para no tener que ingresar datos manualmente y evitar errores de transcripción

**Criterios de Aceptación**:
1. El sistema se conecta al EHR vía HL7 FHIR
2. Se sincronizan automáticamente: datos demográficos, valores de laboratorio (glucosa, HbA1c), signos vitales (peso, altura, presión arterial)
3. La sincronización ocurre cada 4 horas o se puede forzar manualmente
4. Si hay conflicto entre dato del EHR y dato manual, se prioriza EHR pero se notifica al médico
5. Se muestra timestamp de última sincronización en perfil del paciente
6. Se registra en log cada sincronización exitosa y fallida
7. Si EHR no está disponible, el sistema funciona con datos manuales sin caerse

**Notas Técnicas**:
- Implementar adaptador para Epic, Cerner, Allscripts (principales EHRs)
- Usar FHIR R4 (versión más reciente)
- Queue de sincronización con reintentos automáticos
- Considerar webhook para actualizaciones en tiempo real

**Dependencias**: Ninguna (crítica para MVP)

---

## Epic 5: Seguridad y Compliance

### Historia: Autenticación con Single Sign-On

**ID**: REMED-US-040  
**Prioridad**: Must Have  
**Story Points**: 8  
**Sprint**: 1

**Historia**:  
Como médico del hospital  
Quiero iniciar sesión en ReMedical con mis credenciales del hospital (SSO)  
Para no tener que recordar otra contraseña y cumplir con políticas de seguridad institucionales

**Criterios de Aceptación**:
1. La pantalla de login tiene botón "Iniciar sesión con [Hospital Name]"
2. Al hacer click, se redirige a portal de autenticación del hospital
3. Tras autenticar, se redirige de vuelta a ReMedical con sesión activa
4. La sesión expira tras 30 minutos de inactividad
5. Soporta SAML 2.0 y OAuth 2.0
6. Se registra en log cada login exitoso y fallido
7. Hay opción de "Recordar este dispositivo" que extiende sesión a 7 días

**Notas Técnicas**:
- Integrar con Active Directory del hospital
- Usar biblioteca: Authlib o similar
- Tokens JWT con refresh token

**Dependencias**: Ninguna (crítica para seguridad)

---

### Historia: Control de Acceso Basado en Roles

**ID**: REMED-US-041  
**Prioridad**: Must Have  
**Story Points**: 13  
**Sprint**: 2

**Historia**:  
Como administrador del sistema  
Quiero definir roles y permisos para diferentes tipos de usuarios  
Para controlar quién puede ver y modificar información sensible de pacientes

**Criterios de Aceptación**:
1. Existen roles predefinidos: Admin, Médico, Enfermera, Analista de Datos
2. Admin puede: crear usuarios, asignar roles, ver auditoría completa
3. Médico puede: ver pacientes asignados, calcular predicciones, exportar reportes
4. Enfermera puede: ver datos de pacientes, ingresar datos clínicos, NO calcular predicciones
5. Analista de Datos puede: ver dashboard poblacional con datos anónimos, NO ver pacientes individuales
6. Los permisos se validan tanto en frontend (UI) como backend (API)
7. Si usuario intenta acción no permitida, se muestra mensaje claro y se registra en log

**Notas Técnicas**:
- Implementar RBAC (Role-Based Access Control)
- Tabla de permisos granulares en DB
- Middleware de autorización en cada endpoint de API

**Dependencias**: REMED-US-040 (autenticación)

---

### Historia: Auditoría de Acceso a PHI

**ID**: REMED-US-042  
**Prioridad**: Must Have  
**Story Points**: 8  
**Sprint**: 3

**Historia**:  
Como oficial de compliance HIPAA  
Quiero tener log inmutable de cada acceso a información de salud protegida (PHI)  
Para cumplir con requisitos de auditoría de HIPAA y detectar accesos no autorizados

**Criterios de Aceptación**:
1. Cada vez que un usuario accede al perfil de un paciente, se registra: timestamp, usuario, acción (ver/editar), paciente (ID), IP address
2. Cada predicción calculada se registra con: timestamp, usuario, paciente, resultado
3. Los logs son inmutables (no se pueden editar ni eliminar)
4. Hay interfaz para auditor que permite buscar logs por: usuario, paciente, rango de fechas
5. Se pueden exportar logs en formato CSV para análisis externo
6. Se genera reporte mensual automático de actividad
7. Los logs se retienen por mínimo 7 años (requisito HIPAA)

**Notas Técnicas**:
- Almacenar logs en MongoDB (append-only)
- Considerar servicio externo de logging (AWS CloudWatch Logs)
- Encriptar logs en reposo

**Dependencias**: REMED-US-040 (autenticación), REMED-US-041 (roles)

---

## Epic 6: Usabilidad y Experiencia

### Historia: Tutorial Interactivo para Nuevos Usuarios

**ID**: REMED-US-050  
**Prioridad**: Should Have  
**Story Points**: 5  
**Sprint**: 12

**Historia**:  
Como médico nuevo usando ReMedical por primera vez  
Quiero tener un tutorial guiado paso a paso  
Para aprender a usar las funcionalidades principales sin necesidad de capacitación formal

**Criterios de Aceptación**:
1. Al primer login, se muestra modal "Bienvenido a ReMedical" con opción de "Tomar Tour" o "Saltar"
2. El tour guía a través de: búsqueda de paciente, ver perfil, calcular predicción, entender factores, exportar PDF
3. Usa tooltips y highlights para señalar elementos de UI
4. El usuario puede pausar o saltar el tour en cualquier momento
5. Se puede re-acceder al tour desde menú de ayuda
6. El tour es contextual (se adapta al rol del usuario)
7. Al completar el tour, se marca al usuario como "onboarded"

**Notas Técnicas**:
- Usar biblioteca: Intro.js o Shepherd.js
- Personalizar para diferentes roles

**Dependencias**: Todas las funcionalidades principales deben estar completas

---

### Historia: Notificaciones de Pacientes de Alto Riesgo

**ID**: REMED-US-051  
**Prioridad**: Could Have  
**Story Points**: 8  
**Sprint**: 13

**Historia**:  
Como médico endocrinólogo  
Quiero recibir notificación cuando un paciente mío tiene predicción de alto riesgo  
Para priorizar mi atención en casos que requieren intervención urgente

**Criterios de Aceptación**:
1. Cuando una predicción resulta en riesgo >70% (alto), se envía notificación al médico responsable
2. La notificación aparece en dashboard como badge en icono de campana
3. Al hacer click, se muestra lista de alertas con: paciente, riesgo, fecha
4. Se puede hacer click en alerta para ir directo al perfil del paciente
5. Las alertas se pueden marcar como "Revisada" para removerlas de la lista
6. Opcionalmente, se puede configurar email de notificación (opt-in)
7. Las notificaciones se retienen por 30 días

**Notas Técnicas**:
- Sistema de notificaciones en tiempo real (WebSockets o Server-Sent Events)
- Queue de emails con plantillas

**Dependencias**: REMED-US-010 (predicción)

---

## Gestión del Backlog

### Priorización MoSCoW

**Must Have (40%)**: 45 story points
- Funcionalidades críticas para MVP
- Sin estas, el sistema no es viable

**Should Have (35%)**: 38 story points
- Funcionalidades importantes pero no bloqueantes
- Pueden diferirse a release posterior si hay retrasos

**Could Have (20%)**: 21 story points
- Mejoras deseables que agregan valor
- Implementar si hay tiempo disponible

**Won't Have (5%)**: 8 story points
- Funcionalidades fuera de alcance para este release
- Candidatas para roadmap futuro

### Roadmap de Releases

**Release 1.0 (MVP) - 12 sprints (24 semanas)**:
- Epic 1: Gestión de Pacientes (completo)
- Epic 2: Predicción de Riesgo (completo)
- Epic 3: Reportes (solo PDF)
- Epic 4: Integración EHR (básico)
- Epic 5: Seguridad (completo)

**Release 1.1 - 4 sprints (8 semanas)**:
- Epic 3: Dashboard Poblacional
- Epic 6: Usabilidad (completo)
- Mejoras basadas en feedback de usuarios

**Release 2.0 - Futuro**:
- Integración con más EHRs
- Predicción de otras condiciones (hipertensión, obesidad)
- Mobile app para pacientes

---

## Métricas de Historias de Usuario

**Total de Historias Documentadas**: 15  
**Story Points Totales**: 127  
**Velocity Promedio del Equipo**: 34 SP/sprint  
**Sprints Estimados para MVP**: 12 sprints

**Distribución por Prioridad**:
- Must Have: 9 historias (60%)
- Should Have: 5 historias (33%)
- Could Have: 1 historia (7%)

**Distribución por Epic**:
- Epic 1 (Gestión Pacientes): 3 historias
- Epic 2 (Predicción): 3 historias
- Epic 3 (Reportes): 2 historias
- Epic 4 (Integración): 1 historia
- Epic 5 (Seguridad): 3 historias
- Epic 6 (Usabilidad): 2 historias

---

## Definition of Ready

Una historia está lista para entrar en sprint cuando cumple:
- Tiene criterios de aceptación claros y verificables
- Ha sido estimada por el equipo (Planning Poker)
- No tiene dependencias bloqueantes sin resolver
- Los mockups/wireframes están disponibles (si aplica)
- El Product Owner la ha priorizado
- El equipo técnico la entiende completamente

## Definition of Done

Una historia está completa cuando:
- El código está implementado según criterios de aceptación
- Tiene unit tests con coverage >80%
- Pasó code review (mínimo 2 aprobaciones)
- Está desplegado en ambiente de staging
- El QA ejecutó casos de prueba y aprobó
- La documentación está actualizada
- El Product Owner la aceptó en Sprint Review

---

