# 📐 Cuadernillo I — Bloque II
## Representación y Proximidad: Embeddings y Espacios Métricos

[⬅️ Volver al Índice Maestro](../README.md)

---

## Capítulo 7: El Producto Escalar: La métrica de la similitud

### 7.1. Explicación para "Dummies": El test de la linterna
El Producto Escalar mide la alineación entre dos vectores. En IA, determina si un patrón de entrada coincide con un patrón aprendido (pesos).
* Si la sombra es larga, los dos dibujos están alineados: se parecen mucho.
* Si no hay sombra (son perpendiculares), los dibujos no tienen nada en común.
* Si la sombra va en dirección opuesta, son trazos contradictorios.

En la IA, el producto escalar es el juez que decide: "¿Este grupo de píxeles encaja con mi patrón de 'oreja de gato'?".

### 7.2. Rigor mediante Ejemplo Aplicado: Template Matching
Supongamos que tenemos un **Vector Patrón ($v_p$)** que representa una línea vertical perfecta en nuestra rejilla de $3 \times 3$ (píxeles 2, 5 y 8 encendidos).

**El Escenario:**
Ahora nos llega una **Imagen de Entrada ($v_{in}$)**. Para saber si contiene esa línea, multiplicamos cada píxel de $v_{in}$ por el de $v_p$ y sumamos los resultados.
* Si $v_{in}$ tiene luz en los mismos sitios que $v_p$, los productos serán $1 \times 1 = 1$, sumando puntos positivos.
* Si $v_{in}$ tiene luz donde $v_p$ está oscuro ($0$), el producto es $1 \times 0 = 0$, no aporta nada.

**Relación con la IA:**
Esto es exactamente lo que hace una neurona en su forma más básica. Los **pesos (weights)** de la neurona son el "patrón" ($v_p$) y la **entrada (input)** es el vector $v_{in}$. El producto escalar $v_p \cdot v_{in}$ es el valor que la neurona pasa a la siguiente capa. Si el resultado es alto, la neurona "se activa" porque ha reconocido su patrón en los datos.

### 7.3. Matemática Teórica y Justificación
En un espacio vectorial real $V$, un **Producto Escalar** es una aplicación bilineal $\langle \cdot, \cdot \rangle$ que cumple tres propiedades fundamentales para todos $u, v, w \in V$ y escalares $\alpha, \beta$:

1. **Simetría:** $\langle u, v \rangle = \langle v, u \rangle$.
2. **Linealidad en el primer argumento:** $\langle \alpha u + \beta v, w \rangle = \alpha \langle u, w \rangle + \beta \langle v, w \rangle$.
3. **Definida positiva:** $\langle v, v \rangle \ge 0$, y $\langle v, v \rangle = 0 \iff v = \vec{0}$.

En la base canónica de $\mathbb{R}^n$, se define como:

$$u \cdot v = \sum_{i=1}^n u_i v_i$$

**Justificación:**
¿Por qué estas reglas? La linealidad permite que la red neuronal sea predecible: si duplicas la intensidad de la imagen, la respuesta de la neurona se duplica. La propiedad definida positiva es la que nos permite, en el siguiente capítulo, definir el concepto de "distancia" y "norma". Sin esta estructura, el "paisaje" donde la IA busca el error sería un caos sin fondo.

### 7.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 7.1: La Proyección de Sombra</b></summary>
  <br>
  <img src="../img/bloque-2/fig-07-1-sombra.png" width="100%">
  <p><em>Dos vectores $u$ y $v$ con un ángulo entre ellos. Una línea discontinua cae desde la punta de $u$ hasta $v$, mostrando el segmento de "sombra" que representa el producto escalar.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 7.2: Multiplicación de Píxeles</b></summary>
  <br>
  <img src="../img/bloque-2/fig-07-2-multiplicacion.png" width="100%">
  <p><em>Dos rejillas $3 \times 3$ se superponen. Solo los píxeles que están encendidos en ambas brillan intensamente en una tercera rejilla de "resultado", ilustrando la suma de productos.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 7.3: El Termómetro de la Neurona</b></summary>
  <br>
  <img src="../img/bloque-2/fig-07-3-neurona.png" width="100%">
  <p><em>Un vector de entrada entrando en una neurona, y el producto escalar representado como una barra de energía que sube según la coincidencia.</em></p>
</details>

---

## Capítulo 8: Geometría del Ángulo: La similitud del coseno

### 8.1. Explicación para "Dummies": ¿Hacia dónde miras?
La Similitud del Coseno se centra en la dirección semántica de los vectores, ignorando su magnitud. Es vital para comparar frases o conceptos en modelos de lenguaje.

En la IA, especialmente cuando trabajamos con texto (LLMs), a menudo no nos importa si un documento es corto o largo (magnitud), sino de qué trata (dirección). El ángulo entre dos vectores es la forma en que la IA dice: "No me importa cuánto hables, me importa que hables de lo mismo que yo".

### 8.2. Rigor mediante Ejemplo Aplicado: Embeddings de palabras
Supongamos que representamos conceptos en un espacio de 2 dimensiones: Eje X (Realeza) y Eje Y (Género).

**El Escenario:**
* **Vector "Rey" ($v_r$):** $(10, -2)$ -> Muy real, poco femenino.
* **Vector "Monarca" ($v_m$):** $(20, -4)$ -> Es el mismo concepto, pero el vector es el doble de largo (quizás aparece más veces en el texto).

Si usáramos la distancia normal, "Rey" y "Monarca" parecerían estar lejos. Pero si calculamos el **ángulo**, veremos que es $0^\circ$. Para un motor de búsqueda como el de Google, son el mismo concepto porque "apuntan" en la misma dirección semántica.

**Relación con la IA:**
Esta es la base de la **Similitud del Coseno**. En los modelos tipo Gemini o GPT, las palabras se convierten en vectores de miles de dimensiones. Para saber si dos frases son similares, la red calcula el coseno del ángulo entre ellas. Si el coseno es $1$ (ángulo de $0^\circ$), la IA sabe que el significado es idéntico.

### 8.3. Matemática Teórica y Justificación
En un espacio euclídeo, la relación entre el producto escalar y el ángulo $\theta$ entre dos vectores $u$ y $v$ viene dada por la fórmula:

$$u \cdot v = \|u\| \|v\| \cos(\theta)$$

De aquí despejamos la **Similitud del Coseno**:

$$\text{Similitud}(u, v) = \cos(\theta) = \frac{u \cdot v}{\|u\| \|v\|}$$

**Justificación:**
¿Por qué el coseno?
1. **Normalización:** Al dividir por las normas ($\|u\| \|v\|$), eliminamos la influencia del "tamaño" del vector. El resultado siempre está entre $-1$ y $1$.
2. **Desigualdad de Cauchy-Schwarz:** Esta ley garantiza que $|u \cdot v| \le \|u\| \|v\|$, lo que asegura que el valor del coseno nunca se salga del rango matemático posible.
3. **Independencia de la escala:** En MLOps, esto es vital. Permite comparar vectores de datos que han sido escalados de forma distinta sin perder la relación conceptual.

### 8.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 8.1: La Brújula Semántica</b></summary>
  <br>
  <img src="../img/bloque-2/fig-08-1-brujula.png" width="100%">
  <p><em>Dos vectores de distinta longitud apuntando al mismo punto, con el arco del ángulo $\theta$ resaltado.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 8.2: El Círculo Unitario</b></summary>
  <br>
  <img src="../img/bloque-2/fig-08-2-circulo.png" width="100%">
  <p><em>Varios vectores de distintas longitudes proyectados sobre un círculo de radio 1. Muestra cómo la dirección es lo único que sobrevive a la normalización.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 8.3: Comparación de Cosenos</b></summary>
  <br>
  <img src="../img/bloque-2/fig-08-3-comparacion.png" width="100%">
  <p><em>Tres casos: Vectores paralelos ($\cos=1$), perpendiculares ($\cos=0$) y opuestos ($\cos=-1$).</em></p>
</details>

---

## Capítulo 9: La Norma y la Distancia: L1, L2 y el error espacial

### 9.1. Explicación para "Dummies": El Dron vs. El Taxi
Las normas miden la distancia al error. La Norma $L_2$ (euclídea) castiga errores grandes cuadráticamente, mientras que la Norma $L_1$ (Manhattan) es lineal y favorece soluciones esparsas. Ambas son casos de la Norma $p$ (Minkowski).
* **La Distancia $L_2$ (Euclídea):** Es como un dron. Vuela en línea recta, atravesando edificios. Es la distancia más corta posible "a ojo de pájaro".
* **La Distancia $L_1$ (Manhattan):** Es como un taxi. No puede atravesar edificios, así que tiene que recorrer calles y avenidas (giros de $90^\circ$). La distancia total es la suma de los bloques horizontales y verticales.

En la IA, usamos estas formas de medir para decirle a la máquina qué tan lejos está de la respuesta correcta. Si la máquina falla, le decimos: "Tu error es de magnitud X". Dependiendo de si usamos $L_1$ o $L_2$, la máquina reaccionará de forma muy distinta ante los fallos grandes.

### 9.2. Rigor mediante Ejemplo Aplicado: Funciones de Pérdida
Estás entrenando una IA para predecir el precio de una vivienda. La casa real vale 500.000€. Tu IA predice 450.000€. El error es de 50.000€.

**El Escenario:**
1. **Si usas la Norma $L_1$ (Error Absoluto Medio - MAE):** El error es simplemente $|500.000 - 450.000| = 50.000$. Si mañana la IA falla por 100.000, el error será 100.000. Es lineal y "justo".
2. **Si usas la Norma $L_2$ (Error Cuadrático Medio - MSE):** El error se eleva al cuadrado. Esos 50.000 se vuelven un número astronómico.

**Relación con la IA:**
¿Por qué preferimos casi siempre $L_2$ en Deep Learning? Porque al elevar al cuadrado, **castigamos desproporcionadamente los errores grandes**. La IA tiene pánico a equivocarse por mucho, así que se esfuerza más en corregir los grandes fallos que los pequeños. Sin embargo, si tus datos tienen "ruido" (outliers), $L_1$ es mejor porque no se vuelve loca con un dato extraño.

### 9.3. Matemática Teórica y Justificación
Sea $V$ un espacio vectorial. Una **Norma** es una función $\|\cdot\|: V \to \mathbb{R}$ que asigna un número real no negativo a cada vector, cumpliendo:
1. **No negatividad:** $\|v\| \ge 0$, y $\|v\| = 0 \iff v = \vec{0}$.
2. **Homogeneidad:** $\|\lambda v\| = |\lambda| \|v\|$.
3. **Desigualdad triangular:** $\|u + v\| \le \|u\| + \|v\|$.

La **Norma $p$** general (Minkowski) se define como:

$$\|v\|_p = \left( \sum_{i=1}^n |v_i|^p \right)^{1/p}$$

* **Norma $L_1$ ($p=1$):** $\|v\|_1 = \sum_{i=1}^n |v_i|$. Es la suma de los valores absolutos. Produce "soluciones esparsas" (prefiere poner muchos ceros).
* **Norma $L_2$ ($p=2$):** $\|v\|_2 = \sqrt{\sum_{i=1}^n v_i^2}$. Es la distancia euclídea clásica derivada del producto escalar.

**Justificación:**
La geometría del espacio cambia según la norma. En $L_2$, el conjunto de puntos a distancia 1 del origen es un círculo. En $L_1$, es un rombo. Esta diferencia geométrica es la que causa que las redes neuronales con regularización $L_1$ (Lasso) "apaguen" neuronas innecesarias, mientras que $L_2$ (Ridge) solo las hace muy pequeñas pero no las apaga.

### 9.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 9.1: La Geometría de las Normas (Bolas Unidad)</b></summary>
  <br>
  <img src="../img/bloque-2/fig-09-1-geometria-normas.png" width="100%">
  <p><em>Un gráfico comparativo mostrando que "un metro" en $L_2$ es un círculo, pero en $L_1$ es un diamante inclinado.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 9.2: El camino del Taxi vs el Dron</b></summary>
  <br>
  <img src="../img/bloque-2/fig-09-2-taxi-dron.png" width="100%">
  <p><em>Un mapa tipo rejilla de ciudad con una línea diagonal ($L_2$) y un camino escalonado ($L_1$) conectando dos puntos.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 9.3: Castigo del Error</b></summary>
  <br>
  <img src="../img/bloque-2/fig-09-3-castigo-error.png" width="100%">
  <p><em>Una gráfica de la función $L_2$ frente a $L_1$ para mostrar cómo el error cuadrático explota ante fallos grandes.</em></p>
</details>

---

## Capítulo 10: Ortogonalidad y Proyecciones: Limpiando el ruido

### 10.1. Explicación para "Dummies": La sombra que no miente
Imagina que tienes una linterna y una pared. Si pones un objeto frente a la luz, su sombra en la pared es una **proyección**. Esa sombra es la "versión simplificada" del objeto en el mundo plano de la pared.

Ahora, imagina que tienes dos linternas en ángulos de $90^\circ$. Si un objeto se mueve exactamente en la dirección de la primera luz, su sombra en la segunda pared ni se inmuta. Eso es la **ortogonalidad**: es la independencia total. Si dos cosas son ortogonales, lo que haga una no afecta en absoluto a la otra.

En la IA, usamos proyecciones para proyectar una imagen compleja sobre el "muro" de lo que estamos buscando (por ejemplo, el concepto de "cara"). Todo lo que no se proyecta en ese muro es ruido ortogonal que la máquina debe ignorar.

### 10.2. Rigor mediante Ejemplo Aplicado: Eliminación de Ruido
Supongamos que tenemos un patrón ideal de un número "1" en nuestra rejilla $3 \times 3$, representado por el vector $v_{ideal}$. Pero la imagen que recibe la cámara ($v_{real}$) tiene "ruido": píxeles encendidos que no deberían estar ahí.

**El Escenario:**
* $v_{ideal}$ (El "1" puro).
* $v_{real}$ (El "1" con ruido).

Para "limpiar" la imagen $v_{real}$, calculamos su **proyección** sobre el vector ideal $v_{ideal}$.
La parte de $v_{real}$ que se alinea con $v_{ideal}$ es el "mensaje". La parte de $v_{real}$ que es **ortogonal** a $v_{ideal}$ es el "ruido".

**Relación con la IA:**
Esta es la lógica detrás del **PCA (Análisis de Componentes Principales)**. La IA analiza miles de dimensiones y proyecta los datos sobre aquellas donde la información es más fuerte, descartando las dimensiones ortogonales donde solo hay variaciones aleatorias o ruido. Es como quitar la estática de una radio para escuchar la voz.

### 10.3. Matemática Teórica y Justificación
Dos vectores $u, v$ son **ortogonales** si y solo si su producto escalar es nulo:

$$u \cdot v = 0$$

La **Proyección Ortogonal** de un vector $v$ sobre un vector $u$ (no nulo) es un nuevo vector $\text{proj}_u(v)$ definido por:

$$\text{proj}_u(v) = \frac{v \cdot u}{u \cdot u} u$$

**Justificación:**
1. **Componente Paralela y Perpendicular:** Todo vector $v$ puede descomponerse de forma única como $v = v_{\parallel} + v_{\perp}$, donde $v_{\parallel}$ es paralelo a $u$ y $v_{\perp}$ es ortogonal a $u$ ($v_{\perp} \cdot u = 0$).
2. **Mínima Distancia:** El vector $v_{\parallel}$ es el punto del subespacio generado por $u$ que está a la **distancia mínima** de $v$.
3. **Optimización:** En el entrenamiento de redes neuronales, cuando calculamos el gradiente, estamos buscando proyecciones en el espacio de parámetros. Si el ajuste que intentamos hacer es ortogonal a lo que la red necesita aprender, el progreso será nulo. La ortogonalidad define los límites de lo que una capa puede transmitir a la siguiente.

### 10.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 10.1: La Descomposición del Vector</b></summary>
  <br>
  <img src="../img/bloque-2/fig-10-1-descomposicion.png" width="100%">
  <p><em>Un vector $v$ descomponiéndose en dos flechas: una sobre la línea de $u$ (proyección) y otra vertical a ella (error/ruido).</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 10.2: El Plano de Proyección</b></summary>
  <br>
  <img src="../img/bloque-2/fig-10-2-plano-proyeccion.png" width="100%">
  <p><em>Una nube de puntos 3D siendo "aplastada" sobre un plano 2D, mostrando cómo la proyección simplifica la complejidad.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 10.3: Ortogonalidad en la Rejilla</b></summary>
  <br>
  <img src="../img/bloque-2/fig-10-3-ortogonalidad.png" width="100%">
  <p><em>Dos imágenes $3 \times 3$ que no comparten ningún píxel, ilustrando que su producto escalar es cero.</em></p>
</details>

---

## Capítulo 11: El Proceso de Gram-Schmidt: Fabricando bases de datos puras

### 11.1. Explicación para "Dummies": El carpintero perfeccionista
El proceso de Gram-Schmidt "endereza" vectores para crear una Base Ortonormal, donde cada eje es perpendicular a los demás y tiene longitud unitaria.

El proceso de **Gram-Schmidt** es como tener una sierra de precisión. Coges la primera madera y la dejas tal cual (tu primer eje). Coges la segunda y, como está algo torcida hacia la primera, le cortas exactamente la parte que se inclina hacia ella. Ahora tienes dos maderas perfectamente perpendiculares. Coges la tercera, le cortas lo que se inclina hacia la primera y lo que se inclina hacia la segunda... y así sucesivamente.

Al final, tienes un set de herramientas donde cada una hace un trabajo **único** y no se estorba con las demás. En IA, esto es pasar de una base cualquiera a una **Base Ortonormal**.

### 11.2. Rigor mediante Ejemplo Aplicado: Descorrelación de Características
Supongamos que estamos diseñando una IA para analizar tipos de madera. Tenemos dos sensores:
1. **Sensor A ($v_1$):** Mide la "Densidad".
2. **Sensor B ($v_2$):** Mide "Densidad + Dureza".

El problema es que el Sensor B está "sucio": contiene información que ya nos da el Sensor A. Si metemos ambos datos tal cual a la red, estamos duplicando información (correlación), lo que hace que el entrenamiento sea más lento y propenso a errores.

**El Escenario:**
Aplicamos Gram-Schmidt:
1. Aceptamos la "Densidad" ($v_1$) como nuestro primer eje puro ($u_1 = v_1$).
2. Al Sensor B ($v_2$), le **restamos su proyección** sobre el Sensor A.
3. Lo que queda es la "Dureza Pura", sin rastro de la densidad.

**Relación con la IA:**
Este es el alma de algoritmos como el **Whitening** (Blanqueo de datos). Antes de entrenar, transformamos los datos para que cada dimensión sea independiente (ortogonal) y tenga la misma escala (normalizada). Esto asegura que la red no le dé importancia extra a una variable solo porque tiene números más grandes o porque está repetida.

### 11.3. Matemática Teórica y Justificación
Sea $\{v_1, \dots, v_n\}$ una base de un espacio euclídeo $\mathbb{R}^n$. El proceso de Gram-Schmidt construye una **base ortogonal** $\{u_1, \dots, u_n\}$ mediante el siguiente algoritmo recurrente:

1. $u_1 = v_1$
2. $u_2 = v_2 - \text{proj}_{u_1}(v_2)$
3. $u_3 = v_3 - \text{proj}_{u_1}(v_3) - \text{proj}_{u_2}(v_3)$
4. En general, para el $k$-ésimo vector:

$$u_k = v_k - \sum_{j=1}^{k-1} \text{proj}_{u_j}(v_k)$$

Para obtener una **base ortonormal** $\{e_1, \dots, e_n\}$, simplemente normalizamos cada vector resultante: 

$$e_i = \frac{u_i}{\|u_i\|}$$

**Justificación:**
¿Por qué restar las proyecciones? Porque la proyección $\text{proj}_{u_j}(v_k)$ representa la "parte de $v_k$ que se comporta como $u_j$". Al restarla, estamos forzando que el nuevo vector sea ortogonal a todos los anteriores.
En computación de alto rendimiento (como el entrenamiento en Vertex AI), trabajar con bases ortonormales es una ventaja masiva: las matrices inversas se convierten simplemente en matrices traspuestas ($A^{-1} = A^T$), lo que reduce la carga computacional de forma drástica.

### 11.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 11.1: La resta del vector proyección</b></summary>
  <br>
  <img src="../img/bloque-2/fig-11-1-resta-proyeccion.png" width="100%">
  <p><em>Un diagrama que muestra el vector $v_2$, su proyección sobre $u_1$, y cómo al restarlos surge un nuevo vector $u_2$ formando un ángulo de $90^\circ$.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 11.2: El proceso en cadena</b></summary>
  <br>
  <img src="../img/bloque-2/fig-11-2-cadena.png" width="100%">
  <p><em>Una secuencia de tres pasos (2D a 3D) donde se van "enderezando" los vectores uno a uno.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 11.3: Matriz Correlacionada vs. Matriz Identidad</b></summary>
  <br>
  <img src="../img/bloque-2/fig-11-3-matriz-correlacionada.png" width="100%">
  <p><em>Una visualización de datos "estirados" (correlacionados) que, tras el proceso, se convierten en una esfera perfecta (datos descorrelacionados).</em></p>
</details>
