# 📐 Cuadernillo I — Bloque II
## Representación y Proximidad: Embeddings y Espacios Métricos

> *"En el espacio de embeddings, la cercanía geométrica es el lenguaje secreto de la semántica."*

[⬅️ Volver al Índice Maestro](../README.md)

---

## Capítulo 7 — El Concepto de Embedding (Inmersión)

### Explicación Intuitiva: Traducir conceptos a coordenadas
Un **Embedding** es una función que toma un objeto discreto (una palabra, un cliente, un código de error) y lo sitúa en un espacio vectorial continuo. No es solo una lista de números; es una posición en un "mapa de significados". Si dos palabras están cerca en este mapa, es porque el modelo ha aprendido que comparten un contexto.

### Ejemplo Aplicado: El mapa de las palabras
Si proyectamos las palabras "Rey", "Reina", "Hombre" y "Mujer" en un espacio de embeddings, la distancia y la dirección entre "Rey" y "Hombre" será casi idéntica a la de "Reina" y "Mujer".
**Relación con la IA:** Los modelos como Gemini (Vertex AI) usan embeddings para "entender" que si buscas "calzado deportivo", también te interesan las "zapatillas de running", aunque las palabras sean distintas.

### Rigor Matemático
Sea $D$ un dominio discreto (diccionario). Un embedding es una aplicación $f: D \to \mathbb{R}^n$ donde $n \ll |D|$. Esta aplicación busca preservar las relaciones de proximidad del dominio original en la estructura métrica de $\mathbb{R}^n$.

$$f(\text{palabra}) = \vec{v} \in \mathbb{R}^n$$

La matriz de embedding $E \in \mathbb{R}^{|D| \times n}$ contiene los parámetros entrenables que definen esta proyección.

### Figuras

<details>
<summary><b>🖼️ Figura 7.1 — Proyección semántica</b></summary>
<br>
<img src="../img/bloque-2/fig-07-1-proyeccion.png" width="100%">
<p><em>Un mapa de puntos donde conceptos similares (frutas, vehículos, profesiones) se agrupan en regiones específicas del espacio.</em></p>
</details>

<details>
<summary><b>🖼️ Figura 7.2 — Operaciones con significados</b></summary>
<br>
<img src="../img/bloque-2/fig-07-2-aritmetica-embeddings.png" width="100%">
<p><em>La famosa operación vectorial: $\vec{v}_{\text{Rey}} - \vec{v}_{\text{Hombre}} + \vec{v}_{\text{Mujer}} \approx \vec{v}_{\text{Reina}}$.</em></p>
</details>

---

## Capítulo 8 — La Métrica de Similitud: El Coseno del Ángulo

### Explicación Intuitiva: ¿Hacia dónde miran los datos?
En espacios de IA, el tamaño de los vectores (su norma) suele ser menos importante que su dirección. La similitud del coseno mide el ángulo entre dos vectores. Si el ángulo es pequeño (coseno cercano a 1), los vectores apuntan en la misma dirección: son semánticamente similares.

### Ejemplo Aplicado: Recomendación de artículos
Si un vector representa tus intereses y otro un artículo, la IA calcula el coseno entre ambos. No importa si el artículo es largo o corto (norma), importa si trata de lo mismo (ángulo).

### Rigor Matemático
Dados dos vectores $u, v \in \mathbb{R}^n$, la similitud del coseno se define como el producto escalar normalizado por sus normas:

$$\text{Similitud}(u, v) = \cos(\theta) = \frac{u \cdot v}{\|u\| \|v\|} = \frac{\sum_{i=1}^{n} u_i v_i}{\sqrt{\sum_{i=1}^{n} u_i^2} \sqrt{\sum_{i=1}^{n} v_i^2}}$$

Valores cercanos a 1 implican máxima similitud; 0 implica ortogonalidad (sin relación).

### Figuras

<details>
<summary><b>🖼️ Figura 8.1 — Ángulo vs Distancia</b></summary>
<br>
<img src="../img/bloque-2/fig-08-1-angulo-distancia.png" width="100%">
<p><em>Comparativa entre Distancia Euclídea (línea recta entre puntos) y Similitud del Coseno (ángulo de apertura).</em></p>
</details>

---

## Capítulo 9 — La Maldición de la Dimensión

### Explicación Intuitiva: El vacío del hiperespacio
A medida que añadimos dimensiones (ejes), el volumen del espacio crece tan rápido que los datos se vuelven "escasos". En 1000 dimensiones, casi todos los puntos están a la misma distancia unos de otros, y todos parecen estar en las esquinas del hipercubo. Esto hace que sea muy difícil encontrar patrones sin una cantidad ingente de datos.

### Ejemplo Aplicado: El problema del sobreajuste
Si intentas clasificar solo 10 imágenes usando un espacio de 10.000 dimensiones, la IA encontrará una "frontera" perfecta por puro azar geométrico, pero fallará con la imagen número 11.

### Rigor Matemático
En un hipercubo de dimensión $n$, la distancia media entre dos puntos distribuidos uniformemente tiende a aumentar con $\sqrt{n}$, mientras que la diferencia entre la distancia máxima y mínima se vuelve insignificante comparada con la distancia mínima:

$$\lim_{n \to \infty} \frac{d_{\text{max}} - d_{\text{min}}}{d_{\text{min}}} = 0$$

Esto anula la efectividad de algoritmos basados en vecinos cercanos (k-NN) en altas dimensiones.

### Figuras

<details>
<summary><b>🖼️ Figura 9.1 — Concentración de distancias</b></summary>
<br>
<img src="../img/bloque-2/fig-09-1-concentracion.png" width="100%">
<p><em>Gráfico que muestra cómo, a mayor dimensión, todas las distancias entre puntos se colapsan en un único valor medio.</em></p>
</details>

---

## Capítulo 10 — Reducción de Dimensionalidad y Proyecciones

### Explicación Intuitiva: Sombras que revelan la forma
Como no podemos ver en 768 dimensiones, necesitamos "proyectar" los datos a 2D o 3D para entenderlos. Es como usar la sombra de un objeto complejo para adivinar su estructura. El objetivo es reducir las dimensiones perdiendo la mínima información posible.

### Ejemplo Aplicado: De 1000 sensores a 3 indicadores
En una planta industrial con 1000 sensores, muchos están correlacionados. Reducir dimensiones nos permite ver el "estado de salud" de la planta en un único panel de control con 2 o 3 ejes principales.

### Rigor Matemático
Buscamos una transformación $T: \mathbb{R}^n \to \mathbb{R}^k$ con $k < n$. En técnicas como PCA (Análisis de Componentes Principales), buscamos los autovectores de la matriz de covarianza que maximizan la varianza explicada.

$$z = W^T x$$

Donde $W$ es la matriz de proyección que contiene los componentes principales.

### Figuras

<details>
<summary><b>🖼️ Figura 10.1 — Proyección lineal</b></summary>
<br>
<img src="../img/bloque-2/fig-10-1-proyeccion-pca.png" width="100%">
<p><em>Un conjunto de puntos en 3D siendo "aplastados" sobre un plano 2D de forma que se mantenga la máxima separación entre ellos.</em></p>
</details>

---

## Capítulo 11 — Embeddings en Vertex AI y RAG

### Explicación Intuitiva: La memoria de la IA
Los modelos de lenguaje tienen un límite de "memoria a corto plazo" (ventana de contexto). Para que Gemini pueda responder sobre tus propios documentos, usamos **RAG (Retrieval Augmented Generation)**. Convertimos tus documentos en vectores de embedding y los guardamos en una base de datos vectorial.

### Ejemplo Aplicado: Auditoría de contratos
Cuando preguntas: "¿Qué dice la cláusula de rescisión?", la IA convierte tu pregunta en un vector, busca los fragmentos de contrato cuyos vectores tengan el coseno más alto, y usa esos fragmentos para redactar la respuesta.

### Rigor Matemático
El proceso RAG es un pipeline de búsqueda de vecinos más cercanos (ANN - Approximate Nearest Neighbors). Dado un query $q$, recuperamos el conjunto de documentos $D^*$ tal que:

$$D^* = \arg\max_{d \in \text{BaseDatos}} \frac{f(q) \cdot f(d)}{\|f(q)\| \|f(d)\|}$$

Donde $f$ es el modelo de embedding (como `text-embedding-004` de Vertex AI).

### Figuras

<details>
<summary><b>🖼️ Figura 11.1 — Arquitectura RAG</b></summary>
<br>
<img src="../img/bloque-2/fig-11-1-arquitectura-rag.png" width="100%">
<p><em>Diagrama de flujo: Usuario -> Embedding -> Base de Datos Vectorial -> Contexto -> LLM -> Respuesta.</em></p>
</details>
