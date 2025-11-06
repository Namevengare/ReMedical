# Requisitos No Funcionales - ISO/IEC 25000 (SQuaRE)

---

## Modelo ISO/IEC 25010

8 características de calidad: Adecuación Funcional, Eficiencia de Desempeño, Compatibilidad, Usabilidad, Fiabilidad, Seguridad, Mantenibilidad, Portabilidad.

---



## 1. Adecuación Funcional

### Completitud Funcional

**Definición**: Grado en que el conjunto de funcionalidades cubre todas las tareas y objetivos del usuario.

**Requisito REMED-NFR-001**:
```
ID: REMED-NFR-001
Característica: Adecuación Funcional → Completitud
Descripción: El sistema debe cubrir el 100% de los casos de uso 
críticos identificados en la fase de análisis

Criterio de Medición:
- Casos de uso implementados / Casos de uso totales = 100%

Estado Actual: 18/18 casos de uso críticos implementados (100%)

Método de Verificación:
- Revisión de matriz de trazabilidad
- Testing de cada caso de uso documentado
```

### Corrección Funcional

**Definición**: Grado en que el producto proporciona resultados correctos con el nivel de precisión requerido.

**Requisito REMED-NFR-002**:
```
ID: REMED-NFR-002
Característica: Adecuación Funcional → Corrección
Descripción: El modelo de predicción debe alcanzar accuracy >90% 
y recall >85% en conjunto de validación

Criterio de Medición:
- Accuracy: (TP + TN) / (TP + TN + FP + FN) > 0.90
- Recall: TP / (TP + FN) > 0.85

Estado Actual:
- Accuracy: 91.2%
- Recall: 87.3%
- F1-Score: 89.1%

Dataset de Validación: 10,000 pacientes (20% del total)

Método de Verificación:
- Evaluación con k-fold cross-validation (k=5)
- Testing en dataset independiente no visto por el modelo
- Re-evaluación trimestral con datos nuevos
```

---

## 2. Eficiencia de Desempeño

### Comportamiento Temporal

**Requisito REMED-NFR-010**:
```
ID: REMED-NFR-010
Característica: Eficiencia de Desempeño → Tiempo de Respuesta
Descripción: El sistema debe completar predicción de riesgo en 
<3 segundos para el percentil 95 de las solicitudes

Criterios de Medición:
- P50 (mediana): <2 segundos
- P95 (percentil 95): <3 segundos  
- P99 (percentil 99): <5 segundos

Condiciones de Test:
- Carga: 100 usuarios concurrentes
- Infraestructura: AWS EC2 m5.large (8 vCPU, 32 GB RAM)
- Red: Conexión empresarial típica (100 Mbps)

Resultados de Test de Carga (JMeter):
- P50: 1.8 segundos ✓
- P95: 2.9 segundos ✓
- P99: 4.2 segundos ✓
- Throughput: 350 requests/segundo

Estado: VERIFICADO

Método de Verificación:
- Performance testing con Apache JMeter
- Monitoreo continuo en producción (AWS CloudWatch)
- Alertas automáticas si P95 > 3.5 segundos
```

**Requisito REMED-NFR-011**:
```
ID: REMED-NFR-011
Característica: Eficiencia de Desempeño → Latencia de UI
Descripción: La interfaz debe responder a interacciones del 
usuario en <100ms para mantener percepción de instantaneidad

Criterios:
- Click en botón → feedback visual: <100ms
- Carga de perfil de paciente: <1 segundo
- Búsqueda de paciente (typeahead): <300ms

Resultados Medidos:
- Clicks: 45ms promedio ✓
- Carga de perfil: 850ms promedio ✓  
- Búsqueda typeahead: 280ms promedio ✓

Estado: VERIFICADO

Método de Verificación:
- Chrome DevTools Performance Profiling
- Lighthouse CI en pipeline
- Real User Monitoring (RUM) en producción
```

### Utilización de Recursos

**Requisito REMED-NFR-012**:
```
ID: REMED-NFR-012
Característica: Eficiencia de Desempeño → Uso de Memoria
Descripción: El backend debe operar con uso de memoria <4GB 
bajo carga normal (50 usuarios concurrentes)

Criterios:
- Memoria RAM: <4GB (uso promedio)
- Memoria RAM: <6GB (picos máximos)
- Sin memory leaks detectables en 72 horas de operación continua

Resultados:
- Uso promedio: 3.2GB ✓
- Pico máximo: 4.8GB ✓
- Memory leaks: Ninguno detectado ✓

Estado: VERIFICADO

Método de Verificación:
- Profiling con py-spy y memory_profiler
- Stress testing por 72 horas continuas
- Monitoreo AWS CloudWatch Metrics
```

**Requisito REMED-NFR-013**:
```
ID: REMED-NFR-013
Característica: Eficiencia de Desempeño → Escalabilidad
Descripción: El sistema debe escalar horizontalmente para 
soportar hasta 500 usuarios concurrentes sin degradación

Criterios:
- Arquitectura stateless permite scaling horizontal
- Auto-scaling configurado: 2-10 instancias
- Tiempo de respuesta P95 <4 segundos bajo carga máxima

Test de Escalabilidad:
- Configuración: Load balancer + 4 instancias backend
- Carga simulada: 500 usuarios, 2000 requests/minuto
- Resultado P95: 3.4 segundos ✓

Estado: VERIFICADO
```

---

## 3. Compatibilidad

### Coexistencia

**Requisito REMED-NFR-020**:
```
ID: REMED-NFR-020
Característica: Compatibilidad → Coexistencia con EHR
Descripción: El sistema debe coexistir con sistemas EHR 
existentes sin interferir en su operación normal

Criterios:
- No modificación de base de datos del EHR (solo lectura)
- Integración mediante APIs estándares (HL7 FHIR)
- Operación independiente si EHR está temporalmente offline

Integr aciones Implementadas:
- Epic (HL7 FHIR R4): Probado en Hospital A ✓
- Cerner (HL7 FHIR R4): Probado en Hospital B ✓
- Allscripts (HL7 FHIR R4): En desarrollo

Estado: PARCIALMENTE VERIFICADO

Método de Verificación:
- Testing de integración en ambientes sandbox de EHRs
- Validación en hospitales piloto
- Monitoreo de logs de errores en producción
```

### Interoperabilidad

**Requisito REMED-NFR-021**:
```
ID: REMED-NFR-021
Característica: Compatibilidad → Interoperabilidad
Descripción: El sistema debe intercambiar datos con sistemas 
externos usando estándares abiertos de salud

Estándares Soportados:
- HL7 FHIR R4 (Fast Healthcare Interoperability Resources)
- SNOMED CT (para terminología clínica)
- LOINC (para códigos de laboratorio)
- ICD-10 (para códigos de diagnóstico)

Criterios:
- 100% de datos exportados en formato FHIR válido
- Validación con FHIR Validator oficial
- Documentación de API según especificación OpenAPI 3.0

Estado: VERIFICADO

Método de Verificación:
- Validación con HL7 FHIR Validator
- Conformance testing contra especificación FHIR
- Interop-a-thon (evento de pruebas de interoperabilidad)
```

---

## 4. Usabilidad

### Capacidad de Aprendizaje

**Requisito REMED-NFR-030**:
```
ID: REMED-NFR-030
Característica: Usabilidad → Facilidad de Aprendizaje
Descripción: Un médico sin experiencia previa debe poder generar 
su primera predicción en <10 minutos sin ayuda externa

Criterios de Aceptación:
- Tarea: Buscar paciente, calcular predicción, entender resultado
- Usuarios: 5 médicos sin exposición previa al sistema
- Métrica: Tiempo hasta completar tarea con éxito
- Objetivo: 100% de usuarios en <10 minutos

Resultados de Usability Testing:
- Médico A: 6 min 23 seg ✓
- Médico B: 8 min 15 seg ✓
- Médico C: 7 min 02 seg ✓
- Médico D: 11 min 45 seg ✗ (encontró UI confuso)
- Médico E: 5 min 38 seg ✓

Tasa de Éxito: 80% (objetivo: >90%)

Estado: PARCIALMENTE VERIFICADO (requiere mejoras)

Acciones Correctivas:
- Agregar tutorial interactivo (Intro.js)
- Mejorar affordances de botones principales
- Tooltips contextuales
- Re-test planeado post-mejoras
```

### Accesibilidad

**Requisito REMED-NFR-031**:
```
ID: REMED-NFR-031
Característica: Usabilidad → Accesibilidad
Descripción: El sistema debe cumplir con WCAG 2.1 Level AA para 
accesibilidad de usuarios con discapacidades

Criterios WCAG 2.1 AA:
- Contraste de color mínimo 4.5:1 para texto normal
- Todo funcional accesible por teclado (sin mouse)
- Textos alt para todas las imágenes
- Labels descriptivos en formularios
- Navegación consistente

Resultados de Auditoría (Lighthouse):
- Accessibility Score: 92/100
- Contraste: ✓ Todas las combinaciones pasan
- Keyboard navigation: ✓ Completamente funcional
- Screen reader: ✓ Compatible con NVDA/JAWS

Estado: VERIFICADO

Método de Verificación:
- Google Lighthouse automated audit
- Manual testing con NVDA screen reader
- Keyboard-only navigation testing
```

### Sistema de Ayuda

**Requisito REMED-NFR-032**:
```
ID: REMED-NFR-032
Característica: Usabilidad → Sistema de Ayuda
Descripción: El sistema debe proporcionar ayuda contextual y 
documentación integrada accesible en <2 clics desde cualquier pantalla

Implementación:
- Tooltips en elementos complejos de UI
- Botón "?" en barra de navegación
- Tutorial interactivo para nuevos usuarios
- Centro de ayuda con búsqueda
- Videos de demostración (2-3 minutos cada uno)

Métricas:
- Tiempo promedio para encontrar respuesta: 45 segundos
- Satisfacción con sistema de ayuda: 78% (encuesta post-UAT)

Estado: VERIFICADO
```

---

## 5. Fiabilidad

### Madurez

**Requisito REMED-NFR-040**:
```
ID: REMED-NFR-040
Característica: Fiabilidad → Tasa de Fallos
Descripción: El sistema debe operar con tasa de fallos <0.1% 
en condiciones normales de uso

Criterios:
- MTBF (Mean Time Between Failures): >720 horas (30 días)
- Tasa de transacciones fallidas: <0.1%
- Zero critical bugs en producción (severidad P0)

Resultados (Primer mes en producción):
- Transacciones totales: 45,230
- Transacciones fallidas: 23 (0.05%) ✓
- Bugs críticos: 0 ✓
- Bugs menores: 7 (todos corregidos)

Estado: VERIFICADO

Método de Verificación:
- Monitoreo de logs de aplicación
- Error tracking con Sentry
- Métricas de uptime con AWS CloudWatch
```

### Disponibilidad

**Requisito REMED-NFR-041**:
```
ID: REMED-NFR-041
Característica: Fiabilidad → Disponibilidad
Descripción: El sistema debe mantener disponibilidad de 99.9% 
durante horario laboral (6 AM - 8 PM, zona horaria del hospital)

Criterios:
- Uptime: 99.9% (permite ~43 minutos de downtime/mes)
- Monitoreo 24/7 con alertas automáticas
- SLA (Service Level Agreement) comprometido con hospitales

Resultados (Primeros 3 meses):
- Mes 1: 99.94% uptime ✓
- Mes 2: 99.97% uptime ✓
- Mes 3: 99.91% uptime ✓

Incidentes:
- Total: 3 incidentes
- Downtime total: 78 minutos (distribuidos en 3 meses)
- Causa principal: Mantenimiento programado de AWS

Estado: VERIFICADO

Método de Verificación:
- Pingdom para monitoring externo
- Status page público (status.remedial.com)
- Postmortems de incidentes documentados
```

### Recuperabilidad

**Requisito REMED-NFR-042**:
```
ID: REMED-NFR-042
Característica: Fiabilidad → Recuperación ante Fallos
Descripción: En caso de fallo, el sistema debe recuperarse y 
restaurar datos en <30 minutos (RTO: Recovery Time Objective)

Criterios:
- RTO (Recovery Time Objective): <30 minutos
- RPO (Recovery Point Objective): <15 minutos (pérdida de datos máxima)
- Backups automáticos diarios
- Backups incrementales cada hora

Implementación:
- Base de datos PostgreSQL: replicación asíncrona a standby
- Backups automáticos en AWS S3 (múltiples regiones)
- Runbook de recuperación documentado
- Simulacros de disaster recovery trimestrales

Último Simulacro de DR (Disaster Recovery):
- Fecha: 15 de octubre, 2025
- Escenario: Fallo completo de instancia primaria de BD
- Tiempo de detección: 3 minutos
- Tiempo de recuperación: 18 minutos ✓
- Pérdida de datos: 0 transacciones ✓

Estado: VERIFICADO
```

---

## 6. Seguridad

### Confidencialidad

**Requisito REMED-NFR-050**:
```
ID: REMED-NFR-050
Característica: Seguridad → Encriptación de Datos PHI
Descripción: Todos los datos de información de salud protegida 
(PHI) deben estar encriptados en tránsito y en reposo

Criterios:
- En tránsito: TLS 1.3 con ciphers seguros
- En reposo: AES-256 para base de datos y backups
- Zero datos PHI en logs o archivos temporales sin encriptar

Implementación:
- HTTPS obligatorio (HTTP redirige a HTTPS)
- Certificate: Wildcard SSL con Let's Encrypt
- Configuración TLS: Only TLS 1.2+ (1.3 preferido)
- Database encryption: PostgreSQL con pg_crypto

Auditoría de Seguridad:
- Herramienta: OWASP ZAP + Qualys SSL Labs
- SSL Labs Score: A+ ✓
- Vulnerabilidades: 0 high/critical ✓

Estado: VERIFICADO

Método de Verificación:
- Penetration testing trimestral
- Automated security scans (Snyk, OWASP Dependency Check)
- Manual review de código sensible
```

**Requisito REMED-NFR-051**:
```
ID: REMED-NFR-051
Característica: Seguridad → Control de Acceso (RBAC)
Descripción: El sistema debe implementar control de acceso 
basado en roles con principio de mínimo privilegio

Roles Definidos:
- Admin: Full access (crear usuarios, configuración)
- Médico: Ver pacientes asignados, calcular predicciones
- Enfermera: Ver pacientes, ingresar datos, NO predicciones
- Analista: Ver dashboard poblacional anónimo, NO pacientes individuales

Criterios:
- Validación de permisos en frontend Y backend
- Registro de auditoría de intentos de acceso no autorizados
- Sesiones expiran tras 30 minutos de inactividad

Testing:
- Intentos de privilege escalation: 0 exitosos de 50 intentos ✓
- Cross-user data access: 0 exitosos de 30 intentos ✓

Estado: VERIFICADO

Método de Verificación:
- Penetration testing con focus en authorization bypass
- Automated tests de permisos (pytest)
```

### Integridad

**Requisito REMED-NFR-052**:
```
ID: REMED-NFR-052
Característica: Seguridad → Integridad de Datos
Descripción: El sistema debe prevenir modificación no autorizada 
de datos médicos y mantener trazabilidad completa

Implementación:
- Auditoría de cambios: Quién, qué, cuándo, por qué
- Checksums (hashing) de datos críticos
- Digital signatures para reportes exportados
- Versionado de predicciones (inmutables una vez guardadas)

Criterios:
- 100% de cambios registrados en audit log
- Audit logs inmutables (append-only en MongoDB)
- Detección de tampering en <1 hora

Auditoría:
- Cambios rastreables: 100% ✓
- Intentos de tampering: 0 (en simulación de red adversaria)

Estado: VERIFICADO
```

### Autenticidad

**Requisito REMED-NFR-053**:
```
ID: REMED-NFR-053
Característica: Seguridad → Autenticación Multi-Factor (MFA)
Descripción: Usuarios con acceso a datos sensibles deben usar 
autenticación de dos factores (2FA)

Implementación:
- Fase 1: Single Sign-On con Active Directory del hospital
- Fase 2 (Roadmap): 2FA opcional con TOTP (Google Authenticator)
- Fase 3 (Roadmap): 2FA obligatorio para Admins

Estado Actual:
- SSO implementado: ✓
- 2FA: En desarrollo (release 1.1)

Método de Verificación:
- Integration testing con proveedor de SSO
- Security audit de flujo de autenticación
```

---

## 7. Mantenibilidad

### Modularidad

**Requisito REMED-NFR-060**:
```
ID: REMED-NFR-060
Característica: Mantenibilidad → Arquitectura Modular
Descripción: El sistema debe estar organizado en componentes 
independientes con bajo acoplamiento y alta cohesión

Arquitectura:
- Microservicios: Prediction, Integration, Audit, Notification
- Comunicación: REST APIs + Message Queue (RabbitMQ)
- Base de datos: Por servicio (Database per Service pattern)

Métricas:
- Coupling Between Objects (CBO): Promedio 3.2 (objetivo: <5) ✓
- Cyclomatic Complexity: Promedio 4.8 (objetivo: <10) ✓
- Lines of Code per Module: Max 2,500 (objetivo: <3,000) ✓

Estado: VERIFICADO

Método de Verificación:
- Análisis estático con SonarQube
- Code reviews enfocados en arquitectura
```

### Reusabilidad

**Requisito REMED-NFR-061**:
```
ID: REMED-NFR-061
Característica: Mantenibilidad → Componentes Reutilizables
Descripción: Componentes comunes deben ser reutilizables para 
facilitar expansión a predicción de otras enfermedades

Bibliotecas Compartidas:
- ml_core: Funciones comunes de ML (training, evaluation)
- fhir_client: Cliente HL7 FHIR reutilizable
- ui_components: Biblioteca React de componentes compartidos

Métricas:
- Code reuse: 34% (objetivo: >30%) ✓
- Duplicación de código: 2.1% (objetivo: <5%) ✓

Estado: VERIFICADO
```

### Analizabilidad

**Requisito REMED-NFR-062**:
```
ID: REMED-NFR-062
Característica: Mantenibilidad → Logging y Observabilidad
Descripción: El sistema debe generar logs estructurados y 
métricas que faciliten diagnóstico de problemas

Implementación:
- Logging: Structured logging (JSON) con Python logging
- Nivel de logs: DEBUG, INFO, WARNING, ERROR, CRITICAL
- Métricas: Prometheus para métricas técnicas
- Tracing: Jaeger para distributed tracing
- Dashboards: Grafana para visualización

Criterios:
- 100% de errores logged con stack trace completo
- Logs searchable en Elasticsearch
- Tiempo promedio para diagnosticar bug: <2 horas

Estado: VERIFICADO

Método de Verificación:
- Simulación de bugs comunes y medición de tiempo de diagnóstico
- Review de dashboards con equipo de operaciones
```

### Modificabilidad

**Requisito REMED-NFR-063**:
```
ID: REMED-NFR-063
Característica: Mantenibilidad → Facilidad de Cambio
Descripción: Cambios en requisitos deben poder implementarse sin 
refactoring masivo del código existente

Criterios:
- Test coverage >80% facilita refactoring seguro
- Continuous Integration con tests automatizados
- Tiempo promedio para implementar cambio simple: <1 día

Métricas:
- Test coverage: 84% ✓
- CI/CD: 100% de commits pasan por pipeline ✓
- Lead time for changes: 1.2 días promedio ✓

Estado: VERIFICADO

Método de Verificación:
- Métricas DORA (DevOps Research and Assessment)
- Tracking de tiempo de cambios en Jira
```

### Testabilidad

**Requisito REMED-NFR-064**:
```
ID: REMED-NFR-064
Característica: Mantenibilidad → Cobertura de Tests
Descripción: El código debe tener cobertura de tests automatizados 
>80% para facilitar mantenimiento sin regresiones

Implementación:
- Unit tests: pytest (Python), Jest (TypeScript)
- Integration tests: pytest + Docker
- E2E tests: Cypress
- Performance tests: JMeter

Métricas Actuales:
- Unit test coverage: 84%
- Integration test coverage: 76%
- E2E coverage: 23 flujos críticos ✓
- Total tests: 1,243 unit + 187 integration + 45 E2E

Tiempo de ejecución:
- Unit tests: 3 minutos
- Integration tests: 12 minutos
- E2E tests: 25 minutos
- Total: ~40 minutos (ejecutados en cada PR)

Estado: VERIFICADO
```

---

## 8. Portabilidad

### Adaptabilidad

**Requisito REMED-NFR-070**:
```
ID: REMED-NFR-070
Característica: Portabilidad → Multi-Hospital Deployment
Descripción: El sistema debe poder desplegarse en diferentes 
hospitales con configuración mínima

Implementación:
- Configuration management: Variables de entorno
- Multi-tenancy: Datos de hospitales aislados por tenant_id
- Customización: Logos, colores, disclaimers por hospital

Criterios:
- Tiempo de setup para nuevo hospital: <4 horas
- Zero cambios de código para nuevo cliente

Despliegues Actuales:
- Hospital A: Producción desde agosto 2025
- Hospital B: Producción desde septiembre 2025
- Clínicas C y D: En proceso de onboarding

Estado: VERIFICADO

Método de Verificación:
- Documentación de deployment procedure
- Simulación de setup en ambiente nuevo
```

### Instalabilidad

**Requisito REMED-NFR-071**:
```
ID: REMED-NFR-071
Característica: Portabilidad → Facilidad de Instalación
Descripción: El sistema debe poder instalarse mediante scripts 
automatizados con mínima intervención manual

Implementación:
- Infrastructure as Code: Terraform para AWS
- Containerización: Docker + Docker Compose
- Orchestration: Kubernetes (opcional para deployments grandes)

Criterios:
- Setup automatizado: 1 comando (terraform apply)
- Rollback automatizado si deployment falla
- Zero downtime deployments (blue-green deployment)

Estado: VERIFICADO

Método de Verificación:
- Testing de scripts de deployment en ambiente limpio
- Cronometraje de tiempo de instalación
```

---

## Matriz de Trazabilidad NFR

| ID NFR | Categoría ISO 25010 | Prioridad | Estado | Método Verificación |
|--------|-------------------|-----------|--------|---------------------|
| NFR-001 | Adecuación Funcional | Must Have | Verificado | Matriz trazabilidad |
| NFR-002 | Adecuación Funcional | Must Have | Verificado | ML evaluation |
| NFR-010 | Eficiencia Desempeño | Must Have | Verificado | JMeter load test |
| NFR-011 | Eficiencia Desempeño | Must Have | Verificado | Chrome DevTools |
| NFR-020 | Compatibilidad | Must Have | Parcial | Integration testing |
| NFR-030 | Usabilidad | Must Have | Parcial | Usability testing |
| NFR-031 | Usabilidad | Should Have | Verificado | WCAG audit |
| NFR-040 | Fiabilidad | Must Have | Verificado | Monitoring logs |
| NFR-041 | Fiabilidad | Must Have | Verificado | Uptime monitoring |
| NFR-050 | Seguridad | Must Have | Verificado | Penetration testing |
| NFR-051 | Seguridad | Must Have | Verificado | Security audit |
| NFR-060 | Mantenibilidad | Should Have | Verificado | SonarQube |
| NFR-070 | Portabilidad | Should Have | Verificado | Deployment testing |

---

## Resumen Ejecutivo

**Características Priorizadas**:
1. Seguridad (HIPAA compliance crítico)
2. Eficiencia de Desempeño (médicos necesitan velocidad)
3. Fiabilidad (sistema crítico para salud)
4. Usabilidad (adopción depende de facilidad de uso)

**Estado General**: 89% de NFRs completamente verificados

**Áreas de Mejora**:
- Usabilidad: Tutorial interactivo en desarrollo
- Compatibilidad: Integración con Allscripts pendiente

**Próximos Pasos**:
- Re-test de usabilidad post-mejoras (sprint 13)
- Completar integración Allscripts (sprint 14)
- Auditoría de seguridad anual (Q1 2026)

---
