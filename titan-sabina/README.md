# ⚔️ TITÁN & SABINA
## SaaS Industrial Autopoyético — Gestión Operativa con Inteligencia Artificial

> *"El dato es ley. La IA es el sistema nervioso central. El director decide en 15 minutos."*

---

## ¿Qué es Titán & Sabina?

Titán & Sabina no es un software de gestión. Es un **organismo digital** diseñado para operar como el sistema inmunitario del margen de beneficio de una empresa de campo.

Un ecosistema de microservicios autónomos que captura evidencias en condiciones adversas, las transforma en inteligencia operativa irrefutable, detecta fugas de capital en tiempo real y propone soluciones comerciales automáticas — todo ello con un objetivo de diseño radical: **15 minutos diarios de supervisión directiva**.

El sistema opera sobre **Python + Vertex AI + Google Cloud**, con **BigQuery** como lago de datos transaccional append-only, blockchain en **Polygon** para trazabilidad legal irrefutable y **PWA nativa** con bóveda local para operación offline total.

**Estado actual:** V4.5 en producción activa. Piloto con Piregal — empresa de servicios técnicos para superyates en Vigo.

---

## Arquitectura General
BORDE (Trinchera)
PWA Nativa + IndexedDB + JWT
│
▼
LA ADUANA (api_ingestion)
Pydantic + Secret Manager + Telegram Webhook
│
▼
EL GENETISTA          LA COSECHADORA CIEGA
Vertex AI             IMAP + DKIM/SPF/DMARC
Structured Outputs    Facturas + Audios
│
▼
BIGQUERY
Lago de Datos Transaccional (Append-Only)
│              │              │
▼              ▼              ▼
EL NOTARIO      SABINA         CRONOS
Auditoría       Intel B2B      Planificación
Determinista    OSINT          Dinámica
│
▼
EL ESCRIBANO
PDF + Merkle Root + Polygon Blockchain
│
▼
TELEGRAM CEO
15 min/día de supervisión

---

## Los Cinco Demonios

### ⚗️ 1. El Genetista — Ingesta y Deconstrucción Molecular

Motor de extracción dimensional conectado a **Vertex AI con Structured Outputs**. El modelo devuelve JSON puro — narrativa libre prohibida.

Transforma el caos del lenguaje natural — audios de operarios, facturas, correos — en un **vector de 25 variables rígidas**, una de ellas expandida en más de **1.500 etiquetas semánticas**. No hay alguien responsable de atomizar variables e introducirlas en una app. Un operario habla. Un correo llega. El sistema los deconstruye en moléculas de verdad y los inyecta en el lago de datos.

**Capacidades:**
- Extracción dimensional estricta sin alucinación narrativa
- Cortafuegos financiero por tenant — estrangula la ingesta si el cliente agota su cuota de tokens
- Cosechadora IMAP con escudo criptográfico DKIM/SPF/DMARC
- Detección y aislamiento automático de facturas troyanas (spoofing)
- Sellado de correos procesados con etiqueta `\Seen` para evitar bucles de ingesta

---

### ⚖️ 2. El Notario — Auditoría Determinista

El auditor implacable que cruza los datos de campo con los registros administrativos. **No usa IA en esta fase** — usa Fuzzy Matching en SQL nativo para cruzar entidades con variaciones sintácticas (`"H-25"` vs `"h25"`) sin riesgo de alucinación donde más duele: el dinero.

**Capacidades:**
- Intersección de tokens y Distancia de Edición en SQL nativo
- Validación de proveedores contra lista homologada por tenant
- Detección de desviaciones de presupuesto ajustadas por nivel de confianza de la IA
- Protocolo de urgencia vital — detecta accidente, herido o peligro inminente antes de cualquier otra auditoría (pain_level = 10 inmediato)
- Alertas críticas directas a Telegram cuando el pain_level supera el umbral táctico
- **Time-Travel** — juzga el pasado con las leyes vigentes en la fecha del evento, no con las actuales
- Protocolo de redención — reintenta registros dudosos tras 1 hora sin tabla adicional ni cron job

**Estados de auditoría:**

| Estado | Significado |
|--------|-------------|
| `ACTIVE` | Auditoría superada |
| `FLAGGED` | Alerta detectada — revisión requerida |
| `UNCERTAIN_DATA` | Confianza insuficiente — reintento programado |
| `QUARANTINE` | Violación crítica — bloqueado |
| `DEAD_LETTER` | Fallo tras redención — intervención humana |
| `HUMAN_VERIFIED` | Validado manualmente |

---

### 🕵️ 3. Sabina — Inteligencia B2B

Agente de inteligencia comercial que opera con **sintaxis determinista** — sin bucles de alucinación en cálculo financiero.

**Capacidades:**
- Filtrado OSINT de solvencia de proveedores por CIF
- Descarte automático de morosos antes de proponer soluciones
- Cálculo de descuentos corporativos sobre PVP
- Determinación de ahorro neto antes de enviar la solución estructurada al CEO
- Integración con APIs de distribuidores (Saltoki, Obramat)

---

### 🧠 4. CRONOS — Planificación Dinámica

Motor táctico que elimina la ceguera operativa cruzando governance_rules con human_capital_matrix.

**Capacidades:**
- Asignación de personal según skill_tree real y coste por hora
- Gantt inteligente ajustado al histórico real de consumo extraído del lago de datos
- Aprendizaje continuo — ajusta estimaciones futuras basándose en desviaciones de proyectos previos
- Integración de API meteorológica para veto de fases por condiciones climáticas
- Algoritmo de nocturnidad con fricción temporal 1.2x
- Emparejamiento RRHH — Oficial + Peón según habilidades y disponibilidad real
- Generación de órdenes de trabajo precisas enviadas directamente a los operarios

---

### 📜 5. El Escribano — Trazabilidad Legal Irrefutable

El sellador de inmutabilidad. Genera pruebas legales que aguantan en un tribunal.

**Capacidades:**
- Generación de PDFs de peritaje preventivo inmutables (FPDF)
- Cálculo de Raíz de Merkle por lotes de evidencias
- Anclaje de hash criptográfico en la **Mainnet de Polygon** via Smart Contracts
- Verificación pública — cualquier abogado o perito puede verificar la autenticidad sin acceso al sistema
- Auditoría Time-Travel — capacidad de auditar el pasado con las leyes vigentes en ese momento histórico

---

## Infraestructura de Seguridad

### El Borde — PWA Nativa con Bóveda Local
Captura offline → IndexedDB (TitanEdgeBunker)
│
▼
Service Worker intercepta
pérdida de señal 4G
│
▼
Retención local segura y cifrada
│
▼
Empuje automático al recuperar red

- **Autenticación ciega** — JWT local con WebCrypto API. Operación sin contacto constante con el servidor
- **Fallback acústico** — si el códec OPUS falla, salta automáticamente a WebRTC crudo
- **Presigned URLs** — las Video-Actas pesadas suben directamente a Google Cloud Storage sin pasar por el servidor Python
- **Bloqueo físico** — la app bloquea el uso de galería y emuladores. Solo evidencia capturada en tiempo real
- **GPS forzado** — geolocalización obligatoria en cada evidencia

### La Cosechadora Ciega — Tres Capas de Filtrado
Capa 1: Escudo Criptográfico
DKIM/SPF/DMARC → Rechazo instantáneo de facturas troyanas
Capa 2: Auditoría Determinista (El Notario)
Fuzzy Matching SQL en doble ciego — sin IA, sin alucinación
Capa 3: Procesamiento Vertex AI
Solo ingresan datos pristinos y verificados

La IA se extirpa en fases tempranas — máxima seguridad con coste cero por filtrado.

### Gobernanza Dinámica sin Tocar Código

Las reglas de negocio se inyectan desde tabla de gobernanza. El CEO dicta las reglas. El sistema las aplica sin intervención del desarrollador. Cada regla tiene `valid_from` / `valid_to` — el sistema aplica la ley vigente en la fecha del evento auditado, no la ley actual.

### Autopoiesis — El Código que se Repara a Sí Mismo
Parche Python inyectado
│
▼
AST intercepta y compila en memoria aislada
│
┌────┴────┐
│         │
Válido    Error detectado
│         │
▼         ▼
Desplegado  AUTOPOIESIS SUICIDA
en caliente Parche abortado
Servidor preservado

Motor AST que analiza el código fuente Python en ejecución. Evalúa, compila e inyecta parches en memoria aislada sin reiniciar servidores. Si detecta error de sintaxis activa autopoiesis suicida — aborta el parche y preserva el servidor. **La infraestructura se protege a sí misma de su propio código.**

---

## El Lago de la Verdad — BigQuery

Arquitectura de lago de datos transaccional con garantía append-only. Ningún registro puede modificarse — solo añadirse. La historia es inmutable.

| Variable | Descripción |
|----------|-------------|
| `event_uuid` | Identificador único irrepetible |
| `tenant_id` | Aislamiento multitenant garantizado |
| `meta_payload` | Vector de 25 variables + 1.500 etiquetas |
| `ai_confidence` | Nivel de certidumbre del modelo (0-1) |
| `pain_level` | Nivel de tensión táctica (0-10) |
| `row_status` | Estado de auditoría del Notario |
| `blockchain_merkle_root` | Hash de sellado en Polygon |
| `human_feedback` | Retroalimentación para fine-tuning |
| `feedback_processed` | Control del ciclo de aprendizaje |
| `valid_from / valid_to` | Gobernanza temporal para Time-Travel |

**Motor de búsqueda semántica vectorial:** `ML.DISTANCE` para recuperación Top-5 de reglas de gobernanza relevantes por contexto.

**Rolling Baseline en BQ ML:** detección automática de anomalías de coste por desviación histórica.

**Buffer de entrenamiento:** pares input/output validados por humanos para fine-tuning futuro del modelo.

---

## Gobernanza Concurrente — CRDT

Resolución matemática de conflictos cuando dos directivos editan el mismo registro en el mismo milisegundo desde IPs distintas.
Edición simultánea detectada
│
▼
Lógica CRDT (Last-Write-Wins)
│
▼
Resolución sin bloqueo de base de datos
│
▼
Registro consistente garantizado

---

## Sectores Objetivo

El sistema es **industrialmente agnóstico**. Mismo core. Configuración por tenant.

| Sector | Casos de uso principales |
|--------|--------------------------|
| **Obras y construcción** | Trazabilidad de fases, control de materiales, peritaje preventivo |
| **Servicios eléctricos** | Órdenes de trabajo, certificación de instalaciones, control de operarios |
| **Superyates** | Trazabilidad técnica irrefutable para armadores y astilleros |
| **Alquiler turístico** | Gestión de incidencias, control de proveedores, reporting a propietarios |
| **Servicios industriales** | Presupuestación inteligente, control OPEX, auditoría de campo |

---

## El Bucle de 15 Minutos
06:00 - 22:00
Operarios capturan evidencias en campo (PWA offline)
│
▼
El Genetista deconstruye en tiempo real
│
▼
El Notario audita y clasifica
│
▼
Sabina propone soluciones comerciales
│
▼
CRONOS ajusta planificación
│
▼
El Escribano sella en Polygon
│
▼
22:00 — Cierre de caja materializado
│
▼
23:00 — CEO recibe resumen ejecutivo en Telegram
│
▼
09:00 — CEO valida en 15 minutos

---

## Modelo de Degradación Elegante

El sistema opera con capacidad reducida cuando algún componente falla — nunca colapsa completamente.

| Componente caído | Comportamiento del sistema |
|------------------|---------------------------|
| Red 4G | Bóveda local activa — evidencias retenidas y empujadas al recuperar |
| Vertex AI | Auditoría determinista SQL continúa sin IA |
| BigQuery | Cola local de evidencias pendientes |
| Telegram | Alertas almacenadas para envío diferido |

---

## Stack Tecnológico

| Componente | Tecnología |
|------------|------------|
| Backend | Python 3.12 |
| IA en nube | Vertex AI — Gemini 2.0 Flash |
| IA local | Llama 3 (Ollama) + Whisper |
| Base de datos | BigQuery (append-only transaccional) |
| Blockchain | Polygon Mainnet (Smart Contracts) |
| Frontend campo | PWA React/Vue + IndexedDB |
| Autenticación | JWT + WebCrypto API + Bcrypt |
| Secretos | Google Secret Manager |
| Despliegue | Cloud Run (Docker python:3.12-slim) |
| Embeddings | text-embedding-005 (Vertex AI) |
| Orquestación | subprocess (demonios independientes) |

---

## Estado del Proyecto — V4.5

- ✅ PWA nativa con bóveda IndexedDB operativa
- ✅ Autenticación JWT Zero-Trust activa
- ✅ El Genetista con Structured Outputs desplegado
- ✅ Cosechadora IMAP con escudo DKIM/SPF/DMARC
- ✅ El Notario con Fuzzy Matching SQL y Time-Travel
- ✅ Sabina con filtrado OSINT y cálculo B2B
- ✅ CRONOS con human_capital_matrix
- ✅ El Escribano con Merkle Root y Polygon
- ✅ BigQuery append-only con búsqueda vectorial
- ✅ Google Secret Manager provisionado
- ✅ Autopoiesis AST implementada
- ✅ Gobernanza CRDT para edición concurrente
- ✅ Alertas Telegram con niveles de urgencia
- 🔄 Piloto activo con Piregal — superyates Vigo
- 🔄 Validación en producción (mayo-octubre 2026)
- ⏳ Comercialización via gestoría +Suárez (Q4 2026)

---

## Modelo Comercial

| Tier | Perfil | Precio/mes |
|------|--------|------------|
| **Básico** | 1-5 operarios, 1-3 obras | 299€ |
| **Profesional** | 6-20 operarios, hasta 10 obras | 699€ |
| **Industrial** | 21-50 operarios, obras ilimitadas | 1.499€ |
| **Enterprise** | +50 operarios, multisede | A medida |

Canal de distribución: gestorías y asesorías sectoriales con comisión recurrente del 20-25%.

---

## Autor

**Sergio Bernárdez Gato**
Ingeniero de Montes · Director Industrial (Grupo Losán, 4 países) · Arquitecto de Sistemas IA

*Titán & Sabina nació de veinte años dirigiendo operaciones industriales en cuatro países y de la certeza de que el margen de beneficio de una empresa de campo se pierde en el caos de la información no estructurada. Este sistema existe para que eso no vuelva a ocurrir.*

---

> *Desarrollado sobre Google Cloud (Vertex AI · BigQuery · Cloud Run · Secret Manager)*
> *Piloto activo: Piregal — Servicios Técnicos para Superyates — Vigo, 2026*
<p align="center">
  <b><a href="https://github.com/bernardezgatosergio-ai">⬅️ Volver al Menú Principal</a></b>
</p
