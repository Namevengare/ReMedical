# Conceptos Básicos de Gestión de Requerimientos

**Documento**: 01 - Fundamentos  
**Versión**: 1.0  
**Fecha**: Noviembre 2025  
**Autor**: Miguel Vengare

---

## Definiciones

### Requerimiento

**Funcionales**: Capacidades específicas del sistema.
- Ejemplo: "El sistema predice riesgo de diabetes tipo 2 con accuracy >90%"

**No Funcionales**: Atributos de calidad y restricciones.
- Ejemplo: "Predicción en <3 segundos (P95)"

### Stakeholders ReMedical

- **Primarios**: Médicos endocrinólogos, pacientes
- **Secundarios**: Administradores hospitalarios, enfermeras
- **Terciarios**: Reguladores (FDA, HIPAA), aseguradoras

---

## Proceso de Gestión de Requerimientos

### 1. Elicitación (Recolección)

Proceso de descubrir requisitos a través de interacción con stakeholders y análisis de fuentes existentes.

**Técnicas aplicadas en ReMedical**:
- Entrevistas estructuradas con 12 médicos endocrinólogos
- Observación de consultas médicas (20 horas)
- Análisis de literatura científica sobre predicción de diabetes
- Workshops con equipos multidisciplinarios

**Resultado**: 47 requisitos funcionales identificados, 23 requisitos no funcionales

### 2. Análisis

Evaluación de requisitos para detectar conflictos, ambigüedades e inconsistencias.

**Ejemplo de conflicto detectado en ReMedical**:
- REQ-F-012: "El sistema debe almacenar historial completo del paciente"
- REQ-NF-008: "Los datos personales deben eliminarse tras 2 años sin actividad"
- **Resolución**: Anonimización de datos para investigación, eliminación de PHI identificable

### 3. Especificación

Documentación formal de requisitos en formato estandarizado.

**Plantilla utilizada en ReMedical**:
```
ID: REMED-RF-001
Título: Predicción de Riesgo de Diabetes
Prioridad: Alta (Must Have)
Descripción: El sistema debe calcular el riesgo de desarrollar diabetes tipo 2 en pacientes adultos (18-75 años) sin diagnóstico previo de diabetes
Criterios de Aceptación:
  1. Accuracy > 90% en conjunto de validación
  2. Recall > 85% para casos de alto riesgo
  3. Tiempo de respuesta < 3 segundos (P95)
  4. Explicabilidad: mostrar top 5 factores contribuyentes
Dependencias: REQ-RF-003 (Integración con EHR)
Restricciones: Cumplimiento HIPAA, FDA Class II
```

### 4. Validación

Confirmación de que los requisitos satisfacen las necesidades reales de los stakeholders.

**Técnicas aplicadas**:
- Revisiones formales con stakeholders médicos
- Prototipos interactivos de baja y alta fidelidad
- Pruebas de aceptación de usuario (UAT) con 8 médicos

### 5. Gestión de Cambios

Los requisitos evolucionan. En ReMedical, el 23% de los requisitos iniciales fueron modificados durante el primer trimestre.

**Proceso de cambio**:
1. Solicitud de cambio formal (Change Request)
2. Análisis de impacto (tiempo, costo, dependencias)
3. Aprobación por comité de cambios
4. Actualización de documentación y trazabilidad
5. Comunicación a equipo

---

## Atributos de Calidad de Requisitos

Un buen requisito debe ser:

**Completo**: Contiene toda la información necesaria para su implementación
- Malo: "El sistema debe ser rápido"
- Bueno: "El sistema debe responder a consultas en menos de 3 segundos para el 95% de las solicitudes con carga de hasta 100 usuarios concurrentes"

**Correcto**: Es técnicamente factible y alineado con objetivos de negocio
- Verificado con arquitecto: "Predicción con XGBoost es factible en infraestructura AWS"

**No Ambiguo**: Tiene una sola interpretación posible
- Malo: "El sistema debe manejar muchos pacientes"
- Bueno: "El sistema debe soportar una base de datos de al menos 500,000 registros de pacientes con tiempos de consulta inferiores a 2 segundos"

**Consistente**: No contradice otros requisitos
- Revisión cruzada identificó 4 inconsistencias en primera iteración

**Verificable**: Se puede probar objetivamente
- Cada requisito tiene criterios de aceptación medibles

**Trazable**: Vinculado a necesidad de negocio y casos de prueba
- Matriz de trazabilidad mantiene 127 vínculos activos

**Priorizado**: Tiene importancia relativa asignada
- Usamos MoSCoW: Must Have (40%), Should Have (35%), Could Have (20%), Won't Have (5%)

---

## Niveles de Requisitos

### Requisitos de Negocio

Objetivos estratégicos de alto nivel.

**Ejemplo ReMedical**:
"Reducir la incidencia de complicaciones por diabetes no diagnosticada en un 20% en poblaciones atendidas durante los próximos 3 años"

### Requisitos de Usuario

Necesidades expresadas desde la perspectiva del usuario final.

**Ejemplo ReMedical** (Dr. González, Endocrinólogo):
"Como médico, quiero ver predicciones de riesgo de diabetes de mis pacientes en menos de 5 clics desde la pantalla principal, para optimizar el tiempo de consulta"

### Requisitos Funcionales

Comportamientos específicos del sistema.

**Ejemplo ReMedical**:
"El sistema debe calcular el score de riesgo utilizando el algoritmo XGBoost entrenado con las variables: edad, IMC, glucosa en ayunas, HbA1c, presión arterial, historial familiar, y actividad física"

### Requisitos No Funcionales

Restricciones y atributos de calidad.

**Ejemplo ReMedical**:
"El sistema debe mantener disponibilidad del 99.9% durante horario laboral (6 AM - 8 PM) en zona horaria del hospital"

---

## Técnicas de Representación

### Lenguaje Natural Estructurado

Usado en SRS de ReMedical. Ventajas: accesible a todos los stakeholders. Desventajas: potencial ambigüedad.

### Historias de Usuario

Formato ágil usado en backlog de ReMedical.

**Template**:
"Como [rol], quiero [funcionalidad], para [beneficio]"

**Ejemplo**:
"Como médico endocrinólogo, quiero exportar el reporte de predicción en formato PDF, para compartirlo con el paciente y archivarlo en su expediente"

### Casos de Uso

Descripciones detalladas de interacciones usuario-sistema. ReMedical tiene 18 casos de uso documentados.

### Modelos Visuales

- Diagramas de flujo de procesos clínicos
- Diagramas de Ishikawa para análisis causal
- Wireframes y prototipos interactivos

---

## Herramientas Utilizadas en ReMedical

### Jira

Gestión de backlog, historias de usuario, seguimiento de sprints.
- 127 historias de usuario creadas
- 89 épicas definidas
- 15 sprints completados

### Confluence

Documentación colaborativa de requisitos.
- 230 páginas de documentación
- 45 diagramas embebidos

### Figma

Diseño de prototipos de alta fidelidad.
- 23 pantallas diseñadas
- 8 flujos de usuario mapeados

### GitHub

Control de versiones de documentación y código.
- 342 commits en rama de requisitos
- 28 pull requests revisados

---

## Métricas de Gestión de Requisitos

**Volatilidad de Requisitos**:
- Requisitos añadidos: 12 (20% del total inicial)
- Requisitos modificados: 14 (23% del total inicial)
- Requisitos eliminados: 3 (5% del total inicial)

**Cobertura de Trazabilidad**:
- Requisitos vinculados a casos de uso: 100%
- Requisitos vinculados a casos de prueba: 94%
- Requisitos vinculados a objetivos de negocio: 100%

**Calidad de Requisitos**:
- Requisitos ambiguos identificados en revisión: 8
- Requisitos incompletos identificados: 5
- Tasa de defectos post-implementación por requisitos mal especificados: 2.3%

---

## Mejores Prácticas Aplicadas

1. **Involucramiento Temprano de Stakeholders**: Entrevistas iniciaron en semana 1 del proyecto

2. **Revisiones Iterativas**: Cada requisito pasó por al menos 2 revisiones formales

3. **Prototipado Rápido**: Mockups validados antes de escribir código

4. **Trazabilidad Bidireccional**: De objetivos de negocio a casos de prueba y viceversa

5. **Gestión de Cambios Formal**: 100% de cambios documentados y aprobados

6. **Documentación Viva**: Actualización continua conforme evoluciona el proyecto

---

## Retos Enfrentados

### Reto 1: Lenguaje Técnico vs. Lenguaje Médico

**Problema**: Médicos utilizan terminología clínica (SNOMED CT), desarrolladores utilizan terminología técnica

**Solución**: Glosario compartido de 150 términos, sesiones de capacitación cruzada

### Reto 2: Requisitos Regulatorios Complejos

**Problema**: FDA y HIPAA imponen restricciones no siempre claras inicialmente

**Solución**: Asesor regulatorio incorporado al equipo desde sprint 2

### Reto 3: Expectativas No Realistas

**Problema**: Stakeholders esperaban sistema de diagnóstico completo en MVP

**Solución**: Educación sobre desarrollo iterativo, priorización con MoSCoW, roadmap visual a 18 meses

---

## Conclusiones

La gestión rigurosa de requerimientos en ReMedical ha sido fundamental para:

- Reducir malentendidos entre stakeholders y equipo técnico
- Identificar conflictos tempranamente antes de implementación
- Mantener alineación con objetivos regulatorios y de negocio
- Facilitar estimación precisa de esfuerzo y tiempo
- Establecer criterios objetivos para pruebas de aceptación

**Inversión en gestión de requisitos**: 340 horas-persona  
**Defectos evitados estimados**: 45 (basado en benchmarks de industria)  
**ROI estimado**: 380% (considerando costo de corrección post-producción)

---

## Referencias

- IEEE 830-1998: Recommended Practice for Software Requirements Specifications
- IREB (International Requirements Engineering Board) Syllabus Foundation Level
- Wiegers, K., & Beatty, J. (2013). Software Requirements, 3rd Edition
- Pohl, K. (2010). Requirements Engineering: Fundamentals, Principles, and Techniques

---

**Historial de Versiones**:
- v1.0 (2025-11-05): Versión inicial completa

**Próxima Revisión**: 2025-12-05
