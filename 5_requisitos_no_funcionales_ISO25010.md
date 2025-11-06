# Requisitos No Funcionales (ISO/IEC 25010 - SQuaRE) - ReMedical

## 1. Introducción a Requisitos No Funcionales

### 1.1 Definición

**Requisitos Funcionales**: "¿QUÉ debe hacer el sistema?"
- Ejemplo: "El sistema debe predecir el riesgo de diabetes"

**Requisitos No Funcionales (NFR)**: "¿CÓMO debe comportarse el sistema?"
- Ejemplo: "El sistema debe predecir en <3 segundos con 99.9% disponibilidad"

### 1.2 Por Qué Son Críticos en ReMedical

| Aspecto | Impacto |
|---------|---------|
| **Performance** | Médicos no esperarán >10 seg → abandono del sistema |
| **Seguridad** | Brecha de datos PHI → multas HIPAA ($50K-$1.5M) |
| **Disponibilidad** | Sistema caído en emergencia → riesgo de vida |
| **Usabilidad** | UI compleja → baja adopción → ROI negativo |
| **Compliance** | No cumplir FDA → no se puede vender |

### 1.3 Características de Buenos NFRs

**SMART + Testeable**:
```
❌ Malo: "El sistema debe ser rápido"
   - No medible, no testeable

✅ Bueno: "El dashboard de predicción debe cargar en <2 segundos 
          para el percentil 95 de requests con 100 usuarios concurrentes,
          medido con JMeter en ambiente de producción"
   - Específico: dashboard de predicción
   - Medible: <2 segundos, P95
   - Alcanzable: benchmarks muestran es posible
   - Relevante: impacta experiencia de usuario
   - Tiempo: aplica en producción
   - Testeable: JMeter puede medir
```

---

## 2. ISO/IEC 25010 - Modelo de Calidad de Producto

### 2.1 Modelo de 8 Características

```
                         ┌──────────────────────┐
                         │   CALIDAD DEL        │
                         │   PRODUCTO SOFTWARE  │
                         └──────────┬───────────┘
                                    │
            ┌───────────────────────┼───────────────────────┐
            │                       │                       │
    ┌───────▼──────┐        ┌───────▼──────┐      ┌───────▼──────┐
    │ FUNCIONALIDAD│        │  EFICIENCIA  │      │ COMPATIBILIDAD│
    │              │        │  DESEMPEÑO   │      │              │
    └──────────────┘        └──────────────┘      └──────────────┘
            │                       │                       │
    ┌───────▼──────┐        ┌───────▼──────┐      ┌───────▼──────┐
    │  USABILIDAD  │        │  CONFIABILIDAD│      │  SEGURIDAD   │
    │              │        │              │      │              │
    └──────────────┘        └──────────────┘      └──────────────┘
            │                       │
    ┌───────▼──────┐        ┌───────▼──────┐
    │MANTENIBILIDAD│        │  PORTABILIDAD│
    │              │        │              │
    └──────────────┘        └──────────────┘
```

---

## 3. Características ISO/IEC 25010 Aplicadas a ReMedical

### 3.1 FUNCTIONAL SUITABILITY (Adecuación Funcional)

**Subcaracterísticas**:
- **Completitud Funcional**: Sistema provee todas las funciones necesarias
- **Corrección Funcional**: Sistema produce resultados correctos
- **Pertinencia Funcional**: Sistema facilita lograr objetivos específicos

#### Ejemplos en ReMedical

```
┌─────────────────────────────────────────────────────────────────┐
│ NFR-FS-001: Completitud Funcional                              │
├─────────────────────────────────────────────────────────────────┤
│ El sistema debe implementar TODAS las funciones especificadas  │
│ en la guía ADA (American Diabetes Association) para evaluación │
│ de riesgo de diabetes tipo 2                                   │
│                                                                 │
│ Funciones requeridas:                                           │
│ ✓ Cálculo de riesgo basado en factores clínicos (8 factores)  │
│ ✓ Evaluación de prediabetes (HbA1c 5.7-6.4%)                  │
│ ✓ Estratificación por edad y etnia                             │
│ ✓ Recomendaciones de screening según ADA guidelines            │
│                                                                 │
│ MEDICIÓN:                                                       │
│ - Checklist de funciones: 100% implementadas                   │
│ - Validación con endocrinólogo: Aprobada                       │
│                                                                 │
│ TESTING:                                                        │
│ - Test cases: TC-FS-001 a TC-FS-008                            │
│ - Resultado: 8/8 pasados ✓                                     │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ NFR-FS-002: Corrección Funcional                               │
├─────────────────────────────────────────────────────────────────┤
│ El modelo ML debe predecir riesgo de diabetes con:             │
│ - Accuracy ≥ 90%                                                │
│ - Precision ≥ 88%                                               │
│ - Recall ≥ 85%                                                  │
│ - F1-Score ≥ 87%                                                │
│ Medido en dataset de validación (10,000 pacientes)             │
│                                                                 │
│ MEDICIÓN:                                                       │
│ Resultados en test set:                                         │
│ - Accuracy: 91.3% ✓                                             │
│ - Precision: 89.7% ✓                                            │
│ - Recall: 88.2% ✓                                               │
│ - F1-Score: 88.9% ✓                                             │
│                                                                 │
│ TESTING:                                                        │
│ - Cross-validation 10-fold                                      │
│ - Validación con casos clínicos reales (N=200)                 │
│ - Concordancia con médicos: 87% ✓                              │
└─────────────────────────────────────────────────────────────────┘
```

---

### 3.2 PERFORMANCE EFFICIENCY (Eficiencia de Desempeño)

**Subcaracterísticas**:
- **Comportamiento Temporal**: Tiempos de respuesta adecuados
- **Utilización de Recursos**: Uso eficiente de CPU, memoria, red
- **Capacidad**: Manejo de volumen de usuarios/datos

#### Ejemplos en ReMedical

```
┌─────────────────────────────────────────────────────────────────┐
│ NFR-PE-001: Tiempo de Respuesta (Comportamiento Temporal)      │
├─────────────────────────────────────────────────────────────────┤
│ REQUISITO:                                                      │
│ El sistema debe calcular predicción de diabetes en:            │
│ - P50 (mediana): <2 segundos                                   │
│ - P95 (percentil 95): <3 segundos                              │
│ - P99 (percentil 99): <5 segundos                              │
│                                                                 │
│ Condiciones:                                                    │
│ - 100 usuarios concurrentes                                     │
│ - Base de datos con 100,000 pacientes                          │
│ - Infraestructura: AWS EC2 m5.large + RDS PostgreSQL           │
│                                                                 │
│ MEDICIÓN (JMeter, 1000 requests):                              │
│ - P50: 1.8 seg ✓                                                │
│ - P95: 2.7 seg ✓                                                │
│ - P99: 4.2 seg ✓                                                │
│                                                                 │
│ TESTING:                                                        │
│ - Performance test: TC-PE-001                                   │
│ - Load test: 500 usuarios simultáneos (stress test)            │
│ - Resultado: Sistema mantiene <3 seg hasta 300 usuarios        │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ NFR-PE-002: Utilización de Recursos                            │
├─────────────────────────────────────────────────────────────────┤
│ REQUISITO:                                                      │
│ El sistema debe operar con:                                     │
│ - CPU: <70% utilización promedio                               │
│ - Memoria: <4 GB RAM por instancia                             │
│ - Ancho de banda: <100 Mbps                                    │
│ - Almacenamiento DB: Crecimiento <50 GB/mes                    │
│                                                                 │
│ MEDICIÓN (CloudWatch, 30 días):                                │
│ - CPU promedio: 42% ✓                                           │
│ - CPU pico: 68% ✓                                               │
│ - Memoria promedio: 2.8 GB ✓                                    │
│ - Memoria pico: 3.9 GB ✓                                        │
│ - Ancho de banda: 45 Mbps ✓                                    │
│ - DB storage: +32 GB/mes ✓                                      │
│                                                                 │
│ OPTIMIZACIONES IMPLEMENTADAS:                                   │
│ - Caching con Redis (TTL 5 min) → -40% CPU                     │
│ - Lazy loading de datos pesados → -25% memoria                 │
│ - Compresión gzip de responses → -60% bandwidth                │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ NFR-PE-003: Capacidad (Scalability)                            │
├─────────────────────────────────────────────────────────────────┤
│ REQUISITO:                                                      │
│ El sistema debe soportar:                                       │
│ - 500 usuarios concurrentes (año 1)                            │
│ - 5,000 usuarios concurrentes (año 3)                          │
│ - 1 millón de pacientes en base de datos                       │
│ - 100,000 predicciones/día                                     │
│                                                                 │
│ Arquitectura para Escalabilidad:                               │
│ - Horizontal scaling con Kubernetes                            │
│ - Load balancer (AWS ELB)                                      │
│ - Database sharding (por región geográfica)                    │
│ - CDN para assets estáticos (CloudFront)                       │
│                                                                 │
│ TESTING:                                                        │
│ - Spike test: 0 → 1000 usuarios en 5 min                       │
│   Resultado: Sistema escaló automáticamente (5→12 pods) ✓      │
│ - Soak test: 500 usuarios durante 24 horas                     │
│   Resultado: No memory leaks, estable ✓                        │
│                                                                 │
│ PROYECCIÓN:                                                     │
│ Con arquitectura actual, soporta hasta 2,000 usuarios          │
│ Para 5,000: Requerirá cluster más grande (costo +$3K/mes)      │
└─────────────────────────────────────────────────────────────────┘
```

---

### 3.3 COMPATIBILITY (Compatibilidad)

**Subcaracterísticas**:
- **Coexistencia**: Funciona junto a otros sistemas
- **Interoperabilidad**: Intercambia información con otros sistemas

#### Ejemplos en ReMedical

```
┌─────────────────────────────────────────────────────────────────┐
│ NFR-CO-001: Interoperabilidad con Sistemas EHR                 │
├─────────────────────────────────────────────────────────────────┤
│ REQUISITO:                                                      │
│ El sistema debe integrarse con los principales EHRs mediante   │
│ estándar FHIR (Fast Healthcare Interoperability Resources) R4  │
│                                                                 │
│ EHRs soportados:                                                │
│ ✓ Epic Systems (FHIR API)                                      │
│ ✓ Cerner (FHIR API)                                            │
│ ✓ Allscripts (FHIR API)                                        │
│ ✓ Athenahealth (REST API + FHIR)                               │
│                                                                 │
│ Datos intercambiados:                                           │
│ - Patient resource (demografía)                                │
│ - Observation resource (laboratorios: glucosa, HbA1c)          │
│ - Condition resource (diagnósticos previos)                    │
│ - MedicationRequest (medicamentos actuales)                    │
│                                                                 │
│ TESTING:                                                        │
│ - Test con sandbox de Epic: ✓ Pasado                           │
│ - Test con sandbox de Cerner: ✓ Pasado                         │
│ - Validación en hospital real (Epic): ✓ 98% éxito             │
│   (2% fallos por timeouts de red, manejados con retry)         │
│                                                                 │
│ CERTIFICACIÓN:                                                  │
│ - HL7 FHIR Connectathon: Participado (Sep 2025)                │
│ - Epic App Orchard: Certificación en proceso                   │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ NFR-CO-002: Compatibilidad de Navegadores                      │
├─────────────────────────────────────────────────────────────────┤
│ REQUISITO:                                                      │
│ La aplicación web debe funcionar correctamente en:             │
│                                                                 │
│ Desktop:                                                        │
│ - Chrome ≥ versión 90                                          │
│ - Firefox ≥ versión 88                                         │
│ - Safari ≥ versión 14                                          │
│ - Edge ≥ versión 90                                            │
│                                                                 │
│ Mobile:                                                         │
│ - iOS Safari ≥ versión 14                                      │
│ - Chrome Android ≥ versión 90                                  │
│                                                                 │
│ Resoluciones soportadas:                                        │
│ - Desktop: 1920×1080, 1366×768, 1440×900                       │
│ - Tablet: 1024×768, 768×1024                                   │
│ - Mobile: 375×667, 414×896                                     │
│                                                                 │
│ TESTING (BrowserStack):                                         │
│ - Chrome 110: ✓ Pasado                                         │
│ - Firefox 110: ✓ Pasado                                        │
│ - Safari 16: ✓ Pasado                                          │
│ - Edge 110: ✓ Pasado                                           │
│ - iOS Safari 16: ✓ Pasado                                      │
│ - Chrome Android 110: ✓ Pasado                                 │
│                                                                 │
│ Issues encontrados:                                             │
│ - Safari 14: Chart.js no renderiza correctamente              │
│   → Solucionado con polyfill                                   │
└─────────────────────────────────────────────────────────────────┘
```

---

### 3.4 USABILITY (Usabilidad)

**Subcaracterísticas**:
- **Reconocimiento de Idoneidad**: Usuario sabe si el sistema sirve para su necesidad
- **Aprendizaje**: Facilidad de aprender a usar el sistema
- **Operabilidad**: Facilidad de operar y controlar
- **Protección contra Errores de Usuario**: Previene errores
- **Estética de UI**: Interfaz agradable
- **Accesibilidad**: Usable por personas con discapacidades

#### Ejemplos en ReMedical

```
┌─────────────────────────────────────────────────────────────────┐
│ NFR-US-001: Facilidad de Aprendizaje (Learnability)            │
├─────────────────────────────────────────────────────────────────┤
│ REQUISITO:                                                      │
│ Un médico sin experiencia previa debe poder:                   │
│ - Completar onboarding en <5 minutos                           │
│ - Realizar su primera predicción en <10 minutos                │
│ - Alcanzar competencia básica en <1 hora                       │
│                                                                 │
│ MEDICIÓN (5 médicos nuevos):                                   │
│ Tiempos de onboarding:                                          │
│ - Dr. A: 4 min 12 seg ✓                                        │
│ - Dr. B: 3 min 45 seg ✓                                        │
│ - Dr. C: 5 min 20 seg ✗ (excede por 20 seg)                   │
│ - Dra. D: 4 min 01 seg ✓                                       │
│ - Dra. E: 3 min 58 seg ✓                                       │
│ Promedio: 4 min 15 seg ✓                                       │
│                                                                 │
│ Primera predicción:                                             │
│ - Promedio: 8 min 38 seg ✓                                     │
│ - Tasa de éxito: 80% (4/5) ⚠                                   │
│                                                                 │
│ MEJORAS IMPLEMENTADAS:                                          │
│ - Tutorial interactivo (tooltips contextuales)                 │
│ - Video de 3 minutos en página de inicio                       │
│ - Modo "Práctica" con datos de prueba                          │
│ - Atajos de teclado documentados (Ctrl+F buscar, etc.)         │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ NFR-US-002: Protección contra Errores de Usuario               │
├─────────────────────────────────────────────────────────────────┤
│ REQUISITO:                                                      │
│ El sistema debe prevenir/mitigar errores comunes de usuarios:  │
│                                                                 │
│ 1. Validación de Entrada en Tiempo Real:                       │
│    - IMC: Solo números 10-60 (rango realista)                  │
│    - Glucosa: 50-400 mg/dL (fuera de rango → advertencia)      │
│    - Edad: 18-120 años                                          │
│    - HbA1c: 4-15% (fuera de rango → advertencia)               │
│                                                                 │
│ 2. Confirmaciones para Acciones Destructivas:                  │
│    - Eliminar predicción: "¿Está seguro?"                      │
│    - Modificar datos históricos: "Esto afectará tendencias"    │
│                                                                 │
│ 3. Autoguardado:                                                │
│    - Formularios se guardan cada 30 segundos                   │
│    - Notificación: "Guardado automáticamente a las 14:35"      │
│                                                                 │
│ 4. Undo/Redo:                                                   │
│    - Historial de últimas 10 acciones                          │
│    - Ctrl+Z para deshacer                                      │
│                                                                 │
│ TESTING:                                                        │
│ - Test con valores inválidos: 25 casos, 25 validaciones ✓      │
│ - Test de confirmaciones: Todas funcionando ✓                  │
│ - Test de autoguardado: Guardado cada 30 seg exacto ✓          │
│                                                                 │
│ MÉTRICAS (30 días en producción):                              │
│ - Errores de validación evitados: 1,234                        │
│ - Acciones revertidas con Undo: 87                             │
│ - Datos recuperados por autoguardado: 23 sesiones              │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ NFR-US-003: Accesibilidad (WCAG 2.1 Nivel AA)                  │
├─────────────────────────────────────────────────────────────────┤
│ REQUISITO:                                                      │
│ El sistema debe cumplir con WCAG 2.1 Nivel AA para permitir    │
│ uso por médicos con discapacidades visuales, auditivas o       │
│ motoras                                                         │
│                                                                 │
│ CRITERIOS WCAG 2.1 AA:                                          │
│                                                                 │
│ 1. Perceptible:                                                 │
│    ✓ Contraste de colores ≥4.5:1 (texto) y ≥3:1 (UI)          │
│    ✓ Texto redimensionable hasta 200% sin scroll horizontal    │
│    ✓ Imágenes tienen alt text descriptivo                      │
│    ✓ Videos tienen subtítulos (tutoriales)                     │
│                                                                 │
│ 2. Operable:                                                    │
│    ✓ Navegación completa con teclado (sin mouse)               │
│    ✓ Orden de tabulación lógico                                │
│    ✓ No hay trampas de teclado                                 │
│    ✓ Sin contenido que parpadea >3 veces/seg (epilepsia)       │
│                                                                 │
│ 3. Comprensible:                                                │
│    ✓ Idioma de página declarado (lang="es")                    │
│    ✓ Navegación consistente en todas las páginas               │
│    ✓ Mensajes de error claros y con sugerencias                │
│    ✓ Etiquetas de formulario asociadas a inputs                │
│                                                                 │
│ 4. Robusto:                                                     │
│    ✓ HTML semántico válido (W3C validator)                     │
│    ✓ Compatible con screen readers (NVDA, JAWS)                │
│    ✓ ARIA labels en componentes complejos                      │
│                                                                 │
│ TESTING:                                                        │
│ - Herramienta: axe DevTools                                    │
│ - Resultado: 0 issues críticos, 2 minor ✓                      │
│ - Test con NVDA screen reader: ✓ Navegación completa posible   │
│ - Contraste verificado: Lighthouse score 100/100 ✓             │
│                                                                 │
│ CERTIFICACIÓN:                                                  │
│ - Auditoría externa: Bureau of Internet Accessibility          │
│ - Resultado: WCAG 2.1 AA Conformant ✓                          │
│ - Certificado válido: 2025-2027                                │
└─────────────────────────────────────────────────────────────────┘
```

---

### 3.5 RELIABILITY (Confiabilidad)

**Subcaracterísticas**:
- **Madurez**: Baja tasa de fallos
- **Disponibilidad**: Sistema operacional cuando se necesita
- **Tolerancia a Fallos**: Opera a pesar de fallos
- **Recuperabilidad**: Puede recuperar datos tras fallo

#### Ejemplos en ReMedical

```
┌─────────────────────────────────────────────────────────────────┐
│ NFR-RE-001: Disponibilidad (Availability)                      │
├─────────────────────────────────────────────────────────────────┤
│ REQUISITO:                                                      │
│ El sistema debe estar disponible:                              │
│ - 99.9% uptime anual (máximo 8.76 horas de downtime/año)       │
│ - 24/7/365 (sin ventanas de mantenimiento planificadas)        │
│ - RTO (Recovery Time Objective): <1 hora                       │
│ - RPO (Recovery Point Objective): <5 minutos de datos          │
│                                                                 │
│ ARQUITECTURA PARA ALTA DISPONIBILIDAD:                          │
│ - Multi-AZ deployment (AWS us-east-1a, us-east-1b)             │
│ - Load balancer con health checks cada 30 seg                  │
│ - Auto-scaling (min 2, max 10 instancias)                      │
│ - Database: RDS Multi-AZ con failover automático               │
│ - Backups: Snapshots cada 6 horas, retention 30 días           │
│                                                                 │
│ MEDICIÓN (12 meses):                                            │
│ Incidentes:                                                     │
│ - Ene-Dic 2025: 3 incidentes                                   │
│   1. Mar 15: 45 min (actualización de infra)                   │
│   2. Jul 22: 120 min (fallo AWS región) → SLA violado          │
│   3. Oct 10: 30 min (DDoS attack mitigado)                     │
│                                                                 │
│ Total downtime: 195 minutos = 3.25 horas                       │
│ Uptime: 99.96% ✓ (supera 99.9%)                                │
│                                                                 │
│ TESTING:                                                        │
│ - Chaos Engineering (Netflix Chaos Monkey): Mensual             │
│ - Failover test: Cada trimestre                                │
│ - Disaster Recovery drill: Anual                               │
│   Último: Oct 2025, RTO=35 min ✓, RPO=2 min ✓                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ NFR-RE-002: Tolerancia a Fallos (Fault Tolerance)              │
├─────────────────────────────────────────────────────────────────┤
│ REQUISITO:                                                      │
│ El sistema debe continuar operando (degraded mode) ante:       │
│ - Fallo de 1 instancia de aplicación                           │
│ - Fallo de servicio externo (EHR API down)                     │
│ - Sobrecarga temporal (spike de tráfico)                       │
│                                                                 │
│ ESTRATEGIAS:                                                    │
│                                                                 │
│ 1. Circuit Breaker para APIs Externas:                         │
│    - Si EHR API falla >50% en 1 min → abrir circuit            │
│    - Fallback: Usar datos cacheados (hasta 24h antigüedad)     │
│    - Notificar a usuario: "Usando datos del último sync"       │
│                                                                 │
│ 2. Graceful Degradation:                                        │
│    - Si modelo ML falla → Usar reglas clínicas simples         │
│    - Si DB read replica falla → Leer de primary (más lento)    │
│    - Si CDN falla → Servir assets desde origin                 │
│                                                                 │
│ 3. Rate Limiting:                                               │
│    - 100 requests/minuto por usuario                           │
│    - 429 Too Many Requests si excede                           │
│    - Retry-After header con backoff exponencial                │
│                                                                 │
│ TESTING:                                                        │
│ - Simular fallo de EHR API: Sistema usó cache ✓                │
│ - Simular fallo de modelo ML: Fallback a reglas ✓              │
│ - Simular spike 10x tráfico: Rate limiting activo ✓            │
│ - Matar 1 de 3 instancias: Load balancer redirigió ✓           │
│                                                                 │
│ MÉTRICAS (producción):                                          │
│ - Circuit breaker abierto: 12 veces (promedio 5 min)           │
│ - Fallback a cache: 234 requests (0.02% de total)              │
│ - Rate limiting triggered: 45 usuarios (spam bots)             │
└─────────────────────────────────────────────────────────────────┘
```

---

### 3.6 SECURITY (Seguridad)

**Subcaracterísticas**:
- **Confidencialidad**: Solo usuarios autorizados acceden a datos
- **Integridad**: Datos no pueden ser modificados sin autorización
- **No Repudio**: Acciones son rastreables y no negables
- **Responsabilidad**: Acciones son atribuibles a usuarios
- **Autenticidad**: Identidad de usuarios es verificable

#### Ejemplos en ReMedical (Crítico en Healthcare)

```
┌─────────────────────────────────────────────────────────────────┐
│ NFR-SE-001: Confidencialidad (HIPAA Compliance)                │
├─────────────────────────────────────────────────────────────────┤
│ REQUISITO:                                                      │
│ Datos PHI (Protected Health Information) deben estar protegidos│
│ según HIPAA Security Rule:                                      │
│                                                                 │
│ 1. Encriptación:                                                │
│    ✓ En tránsito: TLS 1.3 (mínimo TLS 1.2)                     │
│    ✓ En reposo: AES-256                                        │
│    ✓ Backups: Encriptados con AWS KMS                          │
│    ✓ Claves rotadas cada 90 días                               │
│                                                                 │
│ 2. Control de Acceso:                                           │
│    ✓ Role-Based Access Control (RBAC):                         │
│      - Admin: Full access                                      │
│      - Médico: Read/Write pacientes propios                    │
│      - Enfermera: Read-only                                    │
│      - Investigador: Datos anonimizados solo                   │
│    ✓ Principle of Least Privilege                              │
│    ✓ Session timeout: 30 min inactividad                       │
│                                                                 │
│ 3. Anonimización:                                               │
│    ✓ Datos para research: PHI removido (de-identification)     │
│    ✓ Hashing de identificadores (SHA-256)                      │
│    ✓ Logs: No contienen PHI, solo IDs encriptados              │
│                                                                 │
│ TESTING:                                                        │
│ - Penetration testing: Anual por Coalfire                      │
│   Resultado 2025: 0 critical, 1 high (remediado) ✓             │
│ - Vulnerability scanning (Nessus): Mensual                      │
│   Última: 0 critical, 2 medium ✓                               │
│ - HIPAA Security Risk Assessment: Anual                         │
│   Última: Compliant ✓                                          │
│                                                                 │
│ CERTIFICACIÓN:                                                  │
│ - HITRUST CSF Certified (2025-2027) ✓                          │
│ - SOC 2 Type II (2025) ✓                                       │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ NFR-SE-002: Auditoría y No Repudio (Audit Trails)              │
├─────────────────────────────────────────────────────────────────┤
│ REQUISITO (FDA 21 CFR Part 11):                                │
│ El sistema debe mantener registros auditables de:              │
│ - Quién accedió a datos de paciente                            │
│ - Qué datos fueron vistos/modificados                          │
│ - Cuándo ocurrió el acceso                                     │
│ - Desde dónde (IP, dispositivo)                                │
│                                                                 │
│ Logs deben ser:                                                 │
│ - Inmutables (write-once, no pueden ser editados)              │
│ - Retenidos por 7 años (requerimiento legal)                   │
│ - Buscables y generables en <24 horas para auditorías          │
│                                                                 │
│ IMPLEMENTACIÓN:                                                 │
│ - Herramienta: AWS CloudTrail + ElasticSearch                  │
│ - Eventos registrados:                                          │
│   * User login/logout                                          │
│   * View patient record (ID encriptado)                        │
│   * Modify patient data (before/after values)                  │
│   * Run prediction (input parameters)                          │
│   * Export report (recipient, format)                          │
│   * Admin actions (user creation, permission changes)          │
│                                                                 │
│ FORMATO DE LOG:                                                 │
│ {                                                               │
│   "timestamp": "2025-11-05T14:32:11Z",                          │
│   "user_id": "dr_maria_gonzalez",                              │
│   "action": "VIEW_PATIENT",                                     │
│   "patient_id_hash": "a3f7b2c9...",                             │
│   "ip_address": "192.168.1.45",                                 │
│   "device": "Chrome 110/Windows 11",                            │
│   "result": "SUCCESS"                                           │
│ }                                                               │
│                                                                 │
│ TESTING:                                                        │
│ - Log integridad: Hash chain validado ✓                        │
│ - Búsqueda de logs: Query <5 seg para 1M registros ✓           │
│ - Simulacro de auditoría FDA: Logs entregados en 18h ✓         │
│                                                                 │
│ MÉTRICAS:                                                       │
│ - Eventos loggeados: 2.3M/mes                                  │
│ - Storage usado: 45 GB (comprimido)                            │
│ - Auditorías internas: Mensual, 0 issues ✓                     │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ NFR-SE-003: Autenticación Multi-Factor (MFA)                   │
├─────────────────────────────────────────────────────────────────┤
│ REQUISITO:                                                      │
│ Usuarios con acceso a PHI deben autenticarse con ≥2 factores:  │
│ - Factor 1 (algo que sabes): Password                          │
│ - Factor 2 (algo que tienes): TOTP app, SMS, o hardware token  │
│                                                                 │
│ IMPLEMENTACIÓN:                                                 │
│ - SSO con Azure AD / Okta                                      │
│ - MFA obligatorio para:                                         │
│   * Médicos ✓                                                  │
│   * Administradores ✓                                          │
│   * Acceso remoto ✓                                            │
│ - MFA opcional para:                                            │
│   * Investigadores (datos anonimizados)                        │
│                                                                 │
│ OPCIONES MFA:                                                   │
│ 1. Authenticator App (recomendado):                            │
│    - Google Authenticator, Microsoft Authenticator             │
│    - TOTP (Time-based One-Time Password)                       │
│                                                                 │
│ 2. SMS (permitido pero no recomendado por NIST):               │
│    - Códigos de 6 dígitos, válidos 5 minutos                   │
│                                                                 │
│ 3. Hardware Token (para usuarios de alto privilegio):          │
│    - YubiKey, Titan Security Key                               │
│                                                                 │
│ POLÍTICAS:                                                      │
│ - Password: ≥12 caracteres, mayúsculas, minúsculas, números    │
│ - Expiración: Cada 90 días                                     │
│ - Bloqueo: Después de 5 intentos fallidos (15 min)             │
│ - Historial: No reusar últimas 10 passwords                    │
│                                                                 │
│ TESTING:                                                        │
│ - Bypass MFA intento: Bloqueado ✓                              │
│ - Fuerza bruta password: Rate limited ✓                        │
│ - Phishing simulation: 92% de usuarios detectaron ✓            │
│                                                                 │
│ MÉTRICAS (30 días):                                             │
│ - Usuarios con MFA: 237/240 (99%) ✓                            │
│ - MFA failures: 45 (usuarios con teléfono nuevo)               │
│ - Account lockouts: 12 (contraseña olvidada)                   │
└─────────────────────────────────────────────────────────────────┘
```

---

### 3.7 MAINTAINABILITY (Mantenibilidad)

**Subcaracterísticas**:
- **Modularidad**: Sistema dividido en componentes independientes
- **Reusabilidad**: Componentes pueden usarse en otros contextos
- **Analizabilidad**: Facilidad de diagnosticar fallos
- **Modificabilidad**: Facilidad de hacer cambios
- **Testeabilidad**: Facilidad de crear tests

#### Ejemplos en ReMedical

```
┌─────────────────────────────────────────────────────────────────┐
│ NFR-MA-001: Modularidad y Reusabilidad                         │
├─────────────────────────────────────────────────────────────────┤
│ REQUISITO:                                                      │
│ El sistema debe estar organizado en módulos independientes con │
│ interfaces bien definidas, permitiendo:                         │
│ - Desarrollo paralelo por equipos                              │
│ - Reemplazo de componentes sin afectar otros                   │
│ - Reutilización en otros proyectos de salud                    │
│                                                                 │
│ ARQUITECTURA DE MICROSERVICIOS:                                 │
│                                                                 │
│ ┌─────────────────────────────────────────────────┐            │
│ │              API Gateway (Kong)                 │            │
│ └───────────┬──────────────┬──────────────┬───────┘            │
│             │              │              │                    │
│   ┌─────────▼────┐  ┌──────▼──────┐  ┌───▼──────────┐         │
│   │ Auth Service │  │ Patient     │  │ Prediction   │         │
│   │ (Node.js)    │  │ Service     │  │ Service      │         │
│   │              │  │ (Python)    │  │ (Python/ML)  │         │
│   └──────────────┘  └─────────────┘  └──────────────┘         │
│                                                                 │
│   ┌──────────────┐  ┌─────────────┐  ┌──────────────┐         │
│   │ Notification │  │ Report      │  │ Audit        │         │
│   │ Service      │  │ Service     │  │ Service      │         │
│   │ (Go)         │  │ (Python)    │  │ (Node.js)    │         │
│   └──────────────┘  └─────────────┘  └──────────────┘         │
│                                                                 │
│ MÉTRICAS:                                                       │
│ - Coupling (acoplamiento): Bajo ✓                              │
│   Cada servicio puede desplegarse independiente                │
│ - Cohesion (cohesión): Alta ✓                                  │
│   Cada servicio tiene responsabilidad única                    │
│ - Lines of Code por servicio: 2K-5K (tamaño manejable)         │
│                                                                 │
│ REUSABILIDAD:                                                   │
│ - Auth Service: Reutilizado en 2 proyectos internos            │
│ - Patient Service: Fork para proyecto de oncología             │
│ - Librería compartida "remedical-utils": Usada en 5 proyectos  │
│                                                                 │
│ TESTING:                                                        │
│ - Contract testing (Pact): Interfaces validadas ✓              │
│ - Cada servicio tiene suite de tests independiente ✓           │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ NFR-MA-002: Analizabilidad (Observability)                     │
├─────────────────────────────────────────────────────────────────┤
│ REQUISITO:                                                      │
│ El sistema debe proveer herramientas para diagnosticar         │
│ problemas rápidamente:                                          │
│ - Logs centralizados y buscables                               │
│ - Métricas de rendimiento en tiempo real                       │
│ - Trazas distribuidas (distributed tracing)                    │
│ - Alertas automáticas ante anomalías                           │
│                                                                 │
│ STACK DE OBSERVABILIDAD:                                        │
│                                                                 │
│ 1. LOGGING: ELK Stack (Elasticsearch, Logstash, Kibana)        │
│    - Logs estructurados (JSON)                                 │
│    - Retention: 90 días (hot), 1 año (cold)                    │
│    - Búsqueda full-text en <3 segundos                         │
│                                                                 │
│ 2. METRICS: Prometheus + Grafana                               │
│    Dashboards:                                                  │
│    - Golden Signals: Latency, Traffic, Errors, Saturation      │
│    - Business Metrics: Predicciones/hora, tasa de adopción     │
│    - Infrastructure: CPU, memoria, network                     │
│                                                                 │
│ 3. TRACING: Jaeger (OpenTelemetry)                             │
│    - Traces end-to-end de requests                             │
│    - Identificación de bottlenecks                             │
│    - Sampling: 10% en producción, 100% en staging              │
│                                                                 │
│ 4. ALERTING: PagerDuty                                          │
│    Reglas de alerta:                                            │
│    - Error rate >5% durante 5 min → P1 (crítico)               │
│    - Latency P95 >5 seg durante 10 min → P2 (alto)             │
│    - Disk usage >85% → P3 (medio)                              │
│    - Modelo ML drift >10% → P3 (medio)                         │
│                                                                 │
│ TESTING:                                                        │
│ - Simulacro de incident: MTTR (Mean Time To Resolve) = 18 min ✓│
│   Objetivo <30 min                                             │
│ - Log query performance: 2.3 seg promedio ✓                    │
│ - Alert false positive rate: 3% ✓ (objetivo <5%)               │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ NFR-MA-003: Testeabilidad (Test Coverage)                      │
├─────────────────────────────────────────────────────────────────┤
│ REQUISITO:                                                      │
│ El código debe estar diseñado para facilitar testing:          │
│ - Cobertura de código ≥85%                                     │
│ - Tests automatizados en CI/CD                                 │
│ - Mocking de dependencias externas                             │
│ - Tests ejecutables en <10 minutos                             │
│                                                                 │
│ PIRÁMIDE DE TESTING:                                            │
│                                                                 │
│            ┌──────────┐                                         │
│            │   E2E    │  ← 5% (Selenium, Cypress)              │
│            │  (50)    │     [Lento, frágil, costoso]           │
│         ┌──┴──────────┴──┐                                     │
│         │  Integration   │  ← 20% (Pytest, Supertest)         │
│         │     (200)      │     [Medio, medio, medio]          │
│     ┌───┴────────────────┴───┐                                 │
│     │      Unit Tests        │  ← 75% (Pytest, Jest)          │
│     │        (1500)          │     [Rápido, estable, barato]  │
│     └────────────────────────┘                                 │
│                                                                 │
│ MÉTRICAS ACTUALES:                                              │
│ - Line coverage: 87% ✓                                          │
│ - Branch coverage: 82% ✓                                        │
│ - Mutation score: 76% (objetivo >75%) ✓                        │
│                                                                 │
│ ESTRATEGIAS:                                                    │
│ - Dependency Injection: Facilita mocking                       │
│ - Test Doubles: Mocks, Stubs, Fakes para EHR API               │
│ - Test Fixtures: Datos de prueba realistas (anonymized PHI)    │
│ - Containerized Tests: Docker para consistencia                │
│                                                                 │
│ CI/CD PIPELINE:                                                 │
│ - Pre-commit: Linting, formatting (5 seg)                      │
│ - Unit tests: En cada PR (3 min)                               │
│ - Integration tests: En cada merge to main (8 min)             │
│ - E2E tests: Nightly (30 min)                                  │
│ - Performance tests: Weekly (2 horas)                          │
│                                                                 │
│ RESULTADO:                                                      │
│ - Bugs encontrados en producción: 0.8/sprint (industria 3/sprint) ✓│
│ - Regression bugs: 1 en últimos 6 meses ✓                      │
└─────────────────────────────────────────────────────────────────┘
```

---

### 3.8 PORTABILITY (Portabilidad)

**Subcaracterísticas**:
- **Adaptabilidad**: Puede adaptarse a diferentes ambientes
- **Instalabilidad**: Facilidad de instalar en ambientes objetivo
- **Reemplazabilidad**: Puede reemplazar otro software similar

#### Ejemplos en ReMedical

```
┌─────────────────────────────────────────────────────────────────┐
│ NFR-PO-001: Portabilidad Multi-Cloud                           │
├─────────────────────────────────────────────────────────────────┤
│ REQUISITO:                                                      │
│ El sistema debe poder desplegarse en múltiples proveedores     │
│ cloud sin cambios significativos de código:                    │
│ - AWS (primary)                                                │
│ - Azure (secondary/DR)                                         │
│ - GCP (futuro)                                                 │
│ - On-premise (para hospitales con restricciones de datos)      │
│                                                                 │
│ ESTRATEGIA:                                                     │
│ - Containerización con Docker                                  │
│ - Orquestación con Kubernetes (no EKS/AKS específico)          │
│ - Infrastructure as Code (Terraform)                           │
│ - Abstracción de servicios cloud:                              │
│   * Storage: S3 API-compatible (MinIO para on-prem)            │
│   * Database: PostgreSQL (RDS/CloudSQL/on-prem)                │
│   * Queue: RabbitMQ (no SQS-specific)                          │
│                                                                 │
│ TESTING:                                                        │
│ - Deployment en AWS: ✓ Automatizado (Terraform)                │
│ - Deployment en Azure: ✓ Tested en staging                     │
│ - Deployment on-premise: ✓ POC en hospital (VM)                │
│                                                                 │
│ TIEMPO DE MIGRACIÓN:                                            │
│ - AWS → Azure: Estimado 2 semanas (principalmente config)      │
│ - Cloud → On-premise: Estimado 1 mes (networking, security)    │
└─────────────────────────────────────────────────────────────────┘
```

---

## 4. Plantilla de Especificación de NFR para ReMedical

```markdown
## NFR-[ID]: [Título del Requisito]

**Categoría ISO/IEC 25010**: [Característica] → [Subcaracterística]
**Prioridad**: [Alta/Media/Baja]
**Tipo**: [Performance/Security/Usability/Reliability/etc.]

### Descripción
[Descripción detallada del requisito no funcional]

### Rationale (Justificación)
¿Por qué es importante este requisito?
- Impacto en negocio:
- Impacto en usuario:
- Riesgo si no se cumple:

### Métricas y Criterios de Aceptación
- Métrica 1: [valor objetivo]
- Métrica 2: [valor objetivo]
- ...

### Método de Medición
¿Cómo se va a medir que se cumple el requisito?
- Herramientas:
- Frecuencia:
- Responsable:

### Dependencias
- Requisitos relacionados:
- Tecnologías necesarias:
- Restricciones:

### Casos de Prueba
- TC-[ID]: [Descripción]
- TC-[ID]: [Descripción]

### Riesgos
- Riesgo 1: [descripción y mitigación]
- Riesgo 2: [descripción y mitigación]

### Estado
- [ ] Definido
- [ ] Aprobado por stakeholders
- [ ] Implementado
- [ ] Testeado
- [ ] Validado en producción
```

---

## 5. Priorización de NFRs: Matriz de Impacto

```
                    IMPACTO EN USUARIO
                    ▲
                    │
              ALTO  │  Security        Performance
                    │  Usability       Availability
                    │
                    │
            MEDIO   │  Maintainability  Compatibility
                    │  Portability
                    │
                    │
             BAJO   │  Aesthetics
                    │
                    └────────────────────────────────────▶
                      BAJO    MEDIO    ALTO
                         ESFUERZO IMPLEMENTACIÓN

PRIORIDAD:
1. Alto Impacto + Bajo Esfuerzo → HACER PRIMERO (Quick Wins)
2. Alto Impacto + Alto Esfuerzo → ESTRATÉGICO (Planear bien)
3. Bajo Impacto + Bajo Esfuerzo → HACER SI HAY TIEMPO
4. Bajo Impacto + Alto Esfuerzo → NO HACER (No vale la pena)
```

---

## 6. Checklist de Compliance ReMedical

```
☐ ISO/IEC 25010 (Calidad de Software)
   ☐ 8 características principales documentadas
   ☐ NFRs cuantificables para cada característica
   ☐ Tests automatizados para NFRs

☐ FDA (Si aplica como medical device software)
   ☐ 21 CFR Part 11 (Registros electrónicos)
   ☐ IEC 62304 (Software lifecycle)
   ☐ Risk management (ISO 14971)
   ☐ Validation documentation

☐ HIPAA (Privacy & Security)
   ☐ Administrative safeguards
   ☐ Physical safeguards
   ☐ Technical safeguards
   ☐ Business Associate Agreements (BAAs)

☐ ISO 27001 (Information Security)
   ☐ Risk assessment
   ☐ Security controls
   ☐ Incident response plan
   ☐ Annual audits

☐ WCAG 2.1 Level AA (Accessibility)
   ☐ Perceivable
   ☐ Operable
   ☐ Understandable
   ☐ Robust

☐ GDPR (Si opera en EU)
   ☐ Right to access
   ☐ Right to erasure
   ☐ Data portability
   ☐ Privacy by design
```

---

## Referencias

- ISO/IEC 25010:2011 - Systems and software Quality Requirements and Evaluation (SQuaRE)
- ISO/IEC 25023:2016 - Measurement of system and software product quality
- IEEE Std 830-1998 - Recommended Practice for Software Requirements Specifications
- NIST SP 800-53 - Security and Privacy Controls for Information Systems
- FDA Guidance - Software as a Medical Device (SaMD): Clinical Evaluation
- HIPAA Security Rule - 45 CFR Part 164
- WCAG 2.1 - Web Content Accessibility Guidelines
- Bass, L., Clements, P., & Kazman, R. (2012). Software Architecture in Practice (3rd ed.)
