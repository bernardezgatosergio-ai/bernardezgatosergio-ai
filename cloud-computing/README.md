# ☁️ INGENIERÍA EN INTELIGENCIA ARTIFICIAL Y MLOPS
## Google Cloud Platform · Vertex AI · Deep Learning
### Dossier de Dominio Académico y Técnico para la Docencia en IA

> *"La docencia en Inteligencia Artificial exige rigor. No basta con enseñar a consumir modelos preentrenados — es imperativo comprender el sustrato matemático que los gobierna y la infraestructura de nube que permite su escalado."*

---

## Alcance del Dominio

Este documento certifica el dominio técnico en cuatro áreas estructurales que constituyen el núcleo de cualquier programa de formación en IA de nivel universitario o profesional avanzado.
FUNDAMENTOS          ARQUITECTURAS        INFRAESTRUCTURA      ECOSISTEMA
MATEMÁTICOS          DEEP LEARNING        MLOPS (GCP)          GENERATIVO
│                    │                    │                    │
Álgebra Lineal       ANN / CNN / RNN      BigQuery / BQ ML     Gemini Pro/Flash
Cálculo Tensorial    Transformers         Vertex Pipelines     RAG / Embeddings
Teoría Info.         LLMs                 CI/CD Modelos        Agentes / Tools
Optimización         Atención             Model Registry       Structured Output

---

## Bloque 1 — Fundamentos Matemáticos y Algorítmicos

> *"El verdadero aprendizaje automático no es código, es geometría y cálculo multivariable."*

### Espacios Vectoriales y Geometría Euclídea

Operaciones en Rⁿ, producto interno, normas matriciales, distancias, ortogonalidad y proyecciones. Comprensión del espacio donde viven los embeddings de los modelos de lenguaje.

### Álgebra Profunda y el Espacio Dual

Estudio de funcionales lineales y el espacio dual V*. Mapeo de vectores a escalares, isomorfismos y su aplicación en la definición de hiperplanos de separación (SVMs).

### Cálculo Tensorial

Trascender la matriz 2D. Manipulación de tensores de orden n, reglas de contracción de índices (notación de Einstein) y operaciones en lotes (batching) fundamentales para el procesamiento en GPUs/TPUs.

### Optimización Multivariable y Cálculo Diferencial

El motor del aprendizaje. Cálculo de gradientes, matrices Jacobianas y Hessianas. Derivación de la regla de la cadena para la retropropagación algorítmica (Backpropagation) y optimización del descenso de gradiente (SGD, Adam, RMSprop).
Función de pérdida L(θ)
│
▼
Gradiente ∇L(θ) — dirección del descenso
│
┌────┴────┐
│         │
SGD       Adam
Simple    Momento adaptativo

### Teoría de la Información

Entropía de Shannon, Entropía Cruzada (Cross-Entropy) y Divergencia de Kullback-Leibler para la medición de distribuciones de probabilidad en clasificación y modelos generativos.

---

## Bloque 2 — Arquitecturas de Deep Learning

> *"Desde los fundamentos biológicos hasta los modelos fundacionales actuales."*

### Redes Neuronales Artificiales (ANN)

Perceptrón multicapa (MLP), funciones de activación no lineales (ReLU, GELU, Sigmoide) y teoremas de aproximación universal.

### Redes Convolucionales (CNN)

Filtros, strides, pooling (Max/Average) y arquitecturas residuales (ResNet) para evitar el desvanecimiento del gradiente en modelos de visión artificial.

### Redes Recurrentes (RNN/LSTM)

Modelado temporal, celdas de memoria a largo y corto plazo y puertas lógicas para el procesamiento de series temporales y NLP clásico.

### Arquitectura Transformer — El Estado del Arte

Deconstrucción del mecanismo de autoatención (Self-Attention):
Attention(Q, K, V) = softmax(QKᵀ / √dₖ) · V

Atención multicabeza, codificación posicional (Positional Encoding) y modelos secuenciales a gran escala (LLMs).

| Componente | Función |
|------------|---------|
| **Query (Q)** | "¿Qué estoy buscando?" |
| **Key (K)** | "¿Qué ofrezco?" |
| **Value (V)** | "¿Qué información transmito?" |
| **Softmax** | Normalización de relevancia |

---

## Bloque 3 — Google Cloud Computing: Infraestructura MLOps

> *"Alineado con los estándares del Google Cloud Professional Machine Learning Engineer y el Cloud Architect."*

### Arquitectura Base (Core GCP)
IAM (Mínimo Privilegio)
│
┌────┴────────────┐
│                 │
VPC            Cloud Storage
(Red Virtual)    (Almacenamiento)
│
▼
GKE
(Kubernetes Engine)
Despliegues asincrónicos aislados

### Ingeniería de Datos y Lakehouses

Uso avanzado de **BigQuery**:

- Diseño de esquemas append-only con garantía de inmutabilidad
- Particionado y clustering para consultas de alto rendimiento
- Ejecución de modelos ML directamente en base de datos con **BQML**
- Búsqueda semántica vectorial con **ML.DISTANCE**

### MLOps y Ciclo de Vida del Modelo
- Desarrollo
- CI/CD Pipeline
- Vertex AI Pipelines (Kubeflow)
- Model Registry (Versioning)
- Producción
- Monitorización
- Data Drift + Concept Drift

---

## Bloque 4 — Vertex AI y el Ecosistema Generativo

> *"Dominio práctico del stack de inteligencia artificial empresarial de Google."*

### Vertex Custom Training

- Entrenamiento en contenedores personalizados
- Distribución de cargas en clústeres TPU/GPU
- Ajuste de hiperparámetros automatizado (Vizier)

### Vertex AI Search & Conversation — Vector Search

- Implementación de arquitecturas **RAG (Retrieval-Augmented Generation)**:
- Documento / Dato
- Embedding Model (text-embedding-005)
- Vector Index (ANN)
- Vecino más cercano aproximado
- Recuperación Top-K
- Inyección en LLM (contexto sin alucinación)
- Respuesta fundamentada

### Gemini y Structured Outputs

Orquestación avanzada de modelos fundacionales:

| Capacidad | Aplicación |
|-----------|------------|
| **Function Calling / Tools** | Agentes con herramientas externas |
| **Structured Outputs** | Extracción JSON rígido de texto no estructurado |
| **Multimodalidad nativa** | Audio, imagen, vídeo, texto en una sola llamada |
| **Prompt Engineering programático** | Cadenas de razonamiento controlado |

---

## Capacidad Docente Asociada

Este dominio técnico se traduce directamente en capacidad para impartir:

| Asignatura | Nivel | Contenido Principal |
|------------|-------|---------------------|
| **Inteligencia Artificial** | Bachillerato / FP Superior | Fundamentos, aplicaciones, ética |
| **Machine Learning** | Universitario / Máster | Algoritmos, optimización, evaluación |
| **Deep Learning** | Universitario / Máster | Arquitecturas, entrenamiento, despliegue |
| **MLOps y Cloud** | Profesional / Máster | GCP, Vertex AI, pipelines de producción |
| **Matemáticas para IA** | Bachillerato / Universitario | Álgebra lineal, cálculo, probabilidad |
| **IA Generativa** | Todos los niveles | LLMs, RAG, agentes, prompt engineering |

---

## Material Didáctico Propio

### Cuadernillo I — Descubrir la IA a través de la Matemática

45 capítulos estructurados en 9 bloques que llevan al estudiante desde los axiomas del espacio vectorial hasta la geometría del mecanismo de atención de los Transformers.
- Cuadernillo I: Bloque I   → El Espacio de los Datos (Vectores y Bases)
- Cuadernillo I: Bloque II  → Geometría de los Embeddings (Espacios Euclídeos)
- Cuadernillo I: Bloque III → La Neurona como Observador (Espacio Dual)
- Cuadernillo I: Bloque IV  → Dinámica de Capas (Aplicaciones Lineales)
- Cuadernillo II: Bloque V   → El Motor de Procesamiento (Cálculo Tensorial)
- Cuadernillo II: Bloque VI  → Curvatura y Energía (Álgebra Bilineal)
- Cuadernillo II: Bloque VII → El Motor del Aprendizaje (Cálculo y Optimización)
- Cuadernillo II: Bloque VIII→ La Medida del Conocimiento (Teoría de la Información)
- Cuadernillo II: Bloque IX  → Arquitecturas Modernas (Atención y Manifolds)

Cada capítulo sigue una estructura pedagógica de cuatro niveles:
- **Explicación intuitiva** — analogías del mundo real
- **Ejemplo aplicado** — caso concreto con datos reales
- **Rigor matemático** — demostración formal con justificación
- **Herramientas visuales** — figuras sugeridas para el aula

---

## Stack Tecnológico Dominado
- Modelos          →  Gemini 2.0/2.5 Flash/Pro · Llama 3 (Ollama)
- Plataforma       →  Google Cloud Platform · Vertex AI
- Bases de datos   →  BigQuery · Cloud Storage · Lakehouse
- Despliegue       →  Cloud Run · GKE · Docker
- Seguridad        →  Secret Manager · IAM · JWT · WebCrypto
- MLOps            →  Vertex Pipelines · Model Registry · BQ ML
- Embeddings       →  text-embedding-005 · Vector Search (ANN)
- Desarrollo       →  Python 3.12 · FastAPI · Pydantic · AST
- Blockchain       →  Polygon Mainnet · Smart Contracts · Web3

---

## Proyectos en Producción

| Proyecto | Descripción | Stack Principal |
|----------|-------------|-----------------|
| **Caballo de Troya** | Sistema EdTech adaptativo con IA | Gemini Flash 2.5 · BigQuery · Python |
| **Titán & Sabina** | SaaS industrial autopoyético | Vertex AI · BigQuery · Polygon · PWA |

Ambos proyectos en piloto activo — documentación técnica completa disponible en este repositorio.

---

## Autor

**Sergio Bernárdez Gato**
Ingeniero de Montes · DEA · Máster en Formación del Profesorado (STEM)
Director Industrial Internacional · Arquitecto de Sistemas IA

`bernardezgatosergio@gmail.com · Vigo, Galicia`

---

> *"La IA no es magia. Es geometría, cálculo y estadística ejecutados a velocidad industrial.*
> *Enseñar eso — con rigor y con alma — es exactamente lo que hago."*

<p align="center">
  <b><a href="https://github.com/bernardezgatosergio-ai">⬅️ Volver al Menú Principal</a></b>
</p
