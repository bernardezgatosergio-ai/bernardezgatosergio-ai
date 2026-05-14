# 🐎 CABALLO DE TROYA
## Sistema Educativo Adaptativo con Inteligencia Artificial

> *"Diseñado para que el docente vuelva a ser docente — y para que ningún alumno quede atrás sin que nadie lo sepa."*

---

## ¿Qué es Caballo de Troya?

Caballo de Troya no es una aplicación de deberes digitales. Es una **arquitectura pedagógica completa** que integra Inteligencia Artificial adaptativa, telemetría de aprendizaje en tiempo real y metodología colaborativa estructurada en un único ecosistema multitenant diseñado para centros educativos concertados y privados.

El sistema opera sobre **Gemini Flash 2.5** vía API de Google, con **BigQuery** como lago de datos pedagógico y una interfaz de terminal por alumno que convierte cada sesión de aprendizaje en datos científicamente valiosos.

**Estado actual:** Piloto activo en centro concertado de Vigo. TFM del Máster de Formación del Profesorado (USC).

---

## Arquitectura General
CENTRO EDUCATIVO (Tenant)
│
├── Equipo Directivo → PEC + Gobernanza + Dashboard ejecutivo
├── Tutores → Diseño de SDA + Supervisión + Executive Summary
├── Alumnos → Terminal individual + Grupos de escuadrón
└── Familias → Reporte de evolución competencial
│
▼
GEMINI FLASH 2.5
(Tutor IA | Auditor | Paramédico)
│
▼
BIGQUERY
(Lago de datos pedagógico longitudinal)

### Diseño Multitenant

Cada centro opera en un entorno completamente aislado con:

- **PEC propio** inyectado dinámicamente en el sistema
- **Equipo directivo independiente** con panel de supervisión ejecutiva
- **Telemetría blindada** — los datos de un centro no son accesibles desde otro
- **Gobernanza curricular propia** alineada con LOMLOE por centro

---

## Motor de Perfilado IA — El Núcleo

El sistema construye tres perfiles simultáneos por alumno sin intervención del docente y sin etiquetas previas.

### 1. Perfil Neurodivergente (Doble Ciego)

El alumno no sabe que está siendo evaluado. El tutor no introduce sesgos conscientes. El sistema infiere el perfil desde patrones de respuesta en tiempo real:

- **Latencia de respuesta** — tiempo entre exposición al problema y primer intento
- **Tipo de error** — conceptual, procedimental, de comprensión lectora o emocional
- **Patrón de progresión** — lineal, por saltos, regresivo o dependiente de andamiaje
- **Consistencia inter-sesión** — estabilidad del rendimiento en condiciones distintas

El resultado no es un diagnóstico clínico. Es un **mapa de aprendizaje** que el tutor usa para intervenir con precisión, no con intuición.

### 2. Ancla Psicológica

El sistema detecta el **vector motivacional dominante** de cada alumno analizando sus respuestas, elecciones y patrones de engagement. Categorías: NATURALEZA, TECNOLOGÍA, MITOS, LIDERAZGO, SUPERVIVENCIA, CREACIÓN, entre otras.

El ancla no es estática — evoluciona con el alumno. Se usa para contextualizar misiones y maximizar el compromiso emocional con el contenido curricular.

### 3. Punto de Freno

Identifica el **nodo cognitivo exacto** donde el alumno se bloquea de forma recurrente. Diferencia entre:

- **Bloqueo conceptual** — falta de comprensión del fundamento
- **Bloqueo emocional** — ansiedad ante el error o el reto
- **Bloqueo de autoestima** — el alumno cree que no puede antes de intentarlo
- **Bloqueo de base** — prerequisito curricular no adquirido

---

## Los Tres Tipos de Situaciones de Aprendizaje

### SDA Tipo A — El Gimnasio

Refuerzo individual guiado por IA. Equivalente a los deberes tradicionales pero con adaptación continua. La IA no da la respuesta — inyecta la pregunta correcta en el momento correcto para activar el razonamiento del alumno. Cada sesión genera datos de latencia, calidad de razonamiento y evolución del punto de freno.

### SDA Tipo B — Asignatura con Criterio ODS

Situación de aprendizaje vinculada a un saber curricular concreto con un criterio ODS explícito. El alumno trabaja el concepto en contexto real. La IA audita la calidad del razonamiento, no solo la corrección del resultado. Alineamiento automático con descriptores operativos y competencias específicas LOMLOE.

### SDA Tipo C — La Misión Semanal (5 Llaves)

**El núcleo más innovador del sistema.**

Un mismo concepto abordado durante **cinco días consecutivos** desde cinco ángulos distintos. Grupos de **cuatro alumnos de capacidades heterogéneas**.
LUNES     → Llave de Contexto      (¿Dónde estamos?)
MARTES    → Llave de Análisis      (¿Qué está pasando?)
MIÉRCOLES → Llave de Conexión      (¿Cómo se relaciona?)
JUEVES    → Llave de Aplicación    (¿Cómo lo usamos?)
VIERNES   → Llave de Síntesis      (¿Qué hemos construido?)

#### Ceguera Asimétrica

Cada alumno recibe **un fragmento distinto** de la misión. Ninguno puede resolver solo. La solución final requiere que los cuatro coordinen sus fragmentos a través del **Radio de Escuadrón**.

El que más sabe aprende enseñando. El que menos sabe opera sin la presión de la comparación directa.

#### Roles Técnicos Adaptativos

**EXPLORADOR · OPERARIO · GESTOR · ARQUITECTO**

Asignados dinámicamente según el perfil y nivel de avance de cada alumno. Evolucionan con el alumno a lo largo del curso.

---

## El Paramédico IA

Agente de intervención que monitoriza el estado cognitivo y emocional del alumno durante cada sesión. Cuando detecta bloqueo activa la **Transmutación** — reencuadra la misión, cambia el ángulo de ataque, inyecta un andamiaje cognitivo personalizado.

No resuelve. **Desbloquea.**

---

## Detección del Efecto Pigmalión

El sistema cruza las expectativas registradas del tutor sobre cada alumno con los resultados reales de telemetría. Si detecta divergencia sistemática activa una alerta pedagógica.

El tutor está limitando o inflando el potencial del alumno de forma inconsciente. El sistema lo hace visible antes de que cause daño longitudinal.

---

## Soporte al Claustro

### Executive Summary por Sesión
RESUMEN SESIÓN — Grupo 3B
⚠️  5 alumnos bloqueados en el concepto X (bloqueo conceptual)
✅  2 alumnos con progresión excepcional — posible perfil AACC
🔄  3 alumnos con bloqueo emocional — intervención recomendada
📈  Evolución media del grupo: +12% respecto a sesión anterior

El tutor no revisa 30 ejercicios. Recibe datos accionables.

### Gestión de Tutorías

El tutor llega a la reunión con familia con datos objetivos y longitudinales, no con impresiones subjetivas.

### Identificación de Altas Capacidades

El sistema identifica talento oculto mediante patrones de resolución de problemas complejos y saltos lógicos — especialmente en perfiles neurodivergentes que las evaluaciones tradicionales no detectan.

---

## Conexión Familiar

Las familias reciben reportes estructurados de evolución competencial. No la nota numérica estanca — el crecimiento real del alumno en cada saber, sus puntos de freno superados, sus anclas psicológicas activas y su evolución de rol en el escuadrón.

---

## Alineamiento LOMLOE Automático

Cada SDA generada está alineada automáticamente con:

- Descriptores operativos del perfil de salida
- Competencias específicas por área y curso
- Criterios de evaluación vigentes
- Saberes básicos activados por sesión

---

## Telemetría — BigQuery como Lago de Datos Pedagógico

| Variable | Descripción |
|----------|-------------|
| `latencia_respuesta` | Tiempo entre exposición y primer intento |
| `tipo_error` | Clasificación dimensional del error |
| `patron_bloqueo` | Nodo cognitivo de freno identificado |
| `evolucion_rol` | Progresión de rol en el escuadrón |
| `ancora_activa` | Vector motivacional dominante en sesión |
| `confianza_alumno` | Nivel de autoeficacia percibida |
| `calidad_razonamiento` | Score de profundidad argumentativa |
| `pigmalion_alert` | Divergencia expectativa/rendimiento real |

**Los datos son propiedad del centro — no de la plataforma.**

---

## Potencial de Investigación — Proyectos AK2

En 24-36 meses de operación con miles de alumnos genera una base de datos sin precedentes en España:

- Patrones de neurodivergencia no diagnosticada en población escolar
- Efectividad comparada de metodologías colaborativas con IA mediadora
- Correlación entre perfil psicológico y rendimiento académico longitudinal
- Impacto del aprendizaje entre iguales en grupos heterogéneos estructurados
- Detección temprana de altas capacidades en entornos desfavorecidos

Los centros participantes son **coautores de esa investigación** con posibilidad de participar en convocatorias europeas AK2.

---

## Stack Tecnológico

| Componente | Tecnología |
|------------|------------|
| Modelo IA | Gemini Flash 2.5 (Google AI API) |
| Base de datos | BigQuery (lago de datos pedagógico) |
| Backend | Python |
| Arquitectura | Multitenant con aislamiento por centro |
| Estado | Piloto activo — centro concertado Vigo 2025/2026 |
| TFM | Máster Formación del Profesorado USC |

---

## Estado del Proyecto

- ✅ Arquitectura multitenant operativa
- ✅ Motor de perfilado IA con doble ciego activo
- ✅ Tres tipos de SDA implementadas
- ✅ Roles adaptativos (EXPLORADOR / OPERARIO / GESTOR / ARQUITECTO)
- ✅ Ceguera Asimétrica y Radio de Escuadrón funcionando
- ✅ Paramédico IA con Transmutación activa
- ✅ Detección de Efecto Pigmalión implementada
- ✅ Telemetría BigQuery operacional
- ✅ Executive Summary por sesión
- ✅ Dashboard familiar activo
- 🔄 Piloto en curso — centro concertado Vigo
- 🔄 TFM en fase de entrega final

---

## Autor

**Sergio Bernárdez Gato**
Ingeniero de Montes · Máster en Formación del Profesorado (STEM) · Arquitecto de Sistemas IA

*Caballo de Troya nació de una historia personal. Fui un niño que el sistema no supo leer. Esta herramienta existe para que ningún alumno pase desapercibido.*

---

> *Desarrollado como TFM del Máster de Formación del Profesorado de Educación Secundaria*
> *Universidad de Santiago de Compostela — 2025/2026*
