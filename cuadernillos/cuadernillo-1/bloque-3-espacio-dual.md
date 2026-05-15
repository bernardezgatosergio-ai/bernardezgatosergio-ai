# 📐 Cuadernillo I — Bloque III
## La Evaluación del Dato: El Espacio Dual y Covectores

> *"Un vector es una flecha en el espacio. Un covector es la regla graduada que mide esa flecha."*

[⬅️ Volver al Índice Maestro](../README.md)

---

## Capítulo 12 — El Funcional Lineal: La Máquina de Medir

### Explicación Intuitiva: El embudo numérico
Si un vector es un objeto complejo (como una imagen de 1000 píxeles o el perfil de un cliente), un **funcional lineal** es una máquina que traga ese vector complejo y devuelve un único número real. Es un medidor. Puedes tener un funcional que mida el "brillo total" de la imagen, o otro que mida la "probabilidad de impago" del cliente.

### Ejemplo Aplicado: La Neurona Artificial Básica
Antes de aplicar cualquier función de activación no lineal (como ReLU o Sigmoide), una neurona realiza una suma ponderada de sus entradas. Multiplica cada píxel por un peso y suma todo. Esa operación es, en esencia, un funcional lineal actuando sobre el vector de entrada.

### Rigor Matemático
Un funcional lineal (o forma lineal) sobre un espacio vectorial $V$ sobre un cuerpo $\mathbb{R}$ es una aplicación $f: V \to \mathbb{R}$ que conserva la linealidad:

$$f(u + v) = f(u) + f(v)$$
$$f(\lambda v) = \lambda f(v)$$

Para vectores columna $v \in \mathbb{R}^n$, un funcional lineal se representa como un vector fila multiplicando por la izquierda:

$$f(v) = [w_1, w_2, \dots, w_n] \begin{bmatrix} v_1 \\ v_2 \\ \vdots \\ v_n \end{bmatrix} = \sum_{i=1}^{n} w_i v_i$$

### Figuras

<details>
<summary><b>🖼️ Figura 12.1 — El Funcional como Medidor</b></summary>
<br>
<img src="../img/bloque-3/fig-12-1-medidor.png" width="100%">
<p><em>Representación de un vector atravesando un filtro (el funcional) y colapsando en un único escalar en la recta real.</em></p>
</details>

---

## Capítulo 13 — El Espacio Dual ($V^*$): El Universo de los Filtros

### Explicación Intuitiva: El espejo del espacio
Si tienes un espacio vectorial lleno de todas las imágenes posibles, existe un universo paralelo lleno de todos los filtros posibles que pueden evaluar esas imágenes. Ese universo paralelo es el Espacio Dual. A los habitantes del espacio normal los llamamos **vectores**; a los del espacio dual los llamamos **covectores**.

### Ejemplo Aplicado: Los pesos de la red
En Machine Learning, los datos de entrada (las "x") viven en el espacio vectorial $V$. Los parámetros que el modelo aprende (los pesos "w") viven en el Espacio Dual $V^*$. El aprendizaje automático consiste en buscar en el Espacio Dual el covector perfecto que separe correctamente los datos.

### Rigor Matemático
El conjunto de todos los funcionales lineales definidos sobre $V$ forma por sí mismo un espacio vectorial, denominado Espacio Dual y denotado como $V^*$.
Si $V$ tiene dimensión finita $n$, entonces $V^*$ también tiene dimensión finita $n$. 

$$\text{dim}(V) = \text{dim}(V^*) = n$$

Aunque son isomorfos (tienen la misma estructura y dimensión), geométricamente operan de forma distinta. En notación matricial estricta, si $V$ son matrices $n \times 1$ (columnas), $V^*$ son matrices $1 \times n$ (filas).

### Figuras

<details>
<summary><b>🖼️ Figura 13.1 — Vectores vs Covectores</b></summary>
<br>
<img src="../img/bloque-3/fig-13-1-vectores-covectores.png" width="100%">
<p><em>Vectores representados como flechas; covectores representados como familias de hiperplanos paralelos (líneas de contorno) que el vector atraviesa.</em></p>
</details>

---

## Capítulo 14 — La Base Dual: Calibrando los Medidores

### Explicación Intuitiva: Medidores quirúrgicos
Si tienes una base de vectores que construye tu espacio (eje X, eje Y, eje Z), puedes construir una "Base Dual" de medidores que estén calibrados milimétricamente. El primer medidor dual solo detecta movimiento en el eje X e ignora el resto. El segundo solo detecta el eje Y. 

### Ejemplo Aplicado: Extracción de características
Si tu base vectorial representa "Color", "Forma" y "Textura", la base dual son los tres algoritmos exactos que extraen el valor numérico de cada una de esas características de forma aislada, sin que haya interferencia entre ellas (crosstalk).

### Rigor Matemático
Sea $B = \{e_1, e_2, \dots, e_n\}$ una base de $V$. Existe una única base $B^* = \{\phi_1, \phi_2, \dots, \phi_n\}$ de $V^*$ tal que cada funcional $\phi_i$ evalúa a los vectores de la base original según la delta de Kronecker:

$$\phi_i(e_j) = \delta_{ij} = \begin{cases} 1 & \text{si } i = j \\ 0 & \text{si } i \neq j \end{cases}$$

Cualquier funcional $f \in V^*$ se puede expresar como combinación lineal de esta base dual.

### Figuras

<details>
<summary><b>🖼️ Figura 14.1 — La acción de la Base Dual</b></summary>
<br>
<img src="../img/bloque-3/fig-14-1-base-dual.png" width="100%">
<p><em>Un covector $\phi_1$ filtrando un vector $v$, anulando todas sus componentes excepto la correspondiente a $e_1$.</em></p>
</details>

---

## Capítulo 15 — El Aniquilador: Lo que la Máquina no puede ver

### Explicación Intuitiva: El punto ciego
Si tienes un subespacio (una zona concreta de tu universo de datos), el **Aniquilador** es el conjunto de todos los medidores (covectores) que son completamente ciegos a esa zona. Cualquier dato que provenga de ese subespacio dará una medición de cero absoluto en estos medidores.

### Ejemplo Aplicado: Filtrado de ruido
En el procesamiento de señales de IA, si sabemos que el ruido de fondo vive en un subespacio $S$, construimos nuestros filtros utilizando covectores que pertenezcan al aniquilador de $S$. Así, el filtro devolverá $0$ cuando evalúe el ruido, eliminándolo por completo matemáticamente.

### Rigor Matemático
Sea $S$ un subconjunto de $V$. El aniquilador de $S$, denotado como $S^0$, es el subespacio de $V^*$ formado por todos los funcionales que se anulan en $S$:

$$S^0 = \{ f \in V^* \mid f(x) = 0, \forall x \in S \}$$

Si $W$ es un subespacio vectorial de $V$, existe una relación crítica de dimensiones:

$$\text{dim}(W) + \text{dim}(W^0) = \text{dim}(V)$$

### Figuras

<details>
<summary><b>🖼️ Figura 15.1 — El subespacio aniquilador</b></summary>
<br>
<img src="../img/bloque-3/fig-15-1-aniquilador.png" width="100%">
<p><em>Un plano en 3D (el subespacio $W$) y un vector ortogonal (representando al aniquilador $W^0$) que proyecta cualquier punto del plano a cero.</em></p>
</details>

---

## Capítulo 16 — Covectores en IA: La Naturaleza del Gradiente

### Explicación Intuitiva: La pendiente no es una posición
Cuando entrenas una IA, quieres minimizar el error (la Función de Pérdida). Para hacerlo, calculas el Gradiente. El error común es pensar que el gradiente es una flecha de posición. No lo es. El gradiente es una indicación de cómo cambia el error. Por su propia naturaleza matemática, el gradiente no es un vector de datos, es un **covector**.

### Ejemplo Aplicado: Backpropagation en Deep Learning
Durante el paso hacia atrás (backpropagation), lo que fluye por la red neuronal no son datos (vectores), sino gradientes de error (covectores). El gradiente toma una dirección (un cambio en los pesos) y devuelve un escalar (cuánto va a aumentar o disminuir el error).

### Rigor Matemático
La diferencial de una función escalar (como la función de coste $L: \mathbb{R}^n \to \mathbb{R}$) en un punto $x$ no es un vector, es una forma lineal (covector) que pertenece al espacio cotangente (el espacio dual del espacio tangente):

$$dL_x(v) = \lim_{h \to 0} \frac{L(x + hv) - L(x)}{h}$$

El gradiente $\nabla L$ es la representación de este covector mediante el producto escalar. Si operamos de forma rigurosa, los pesos se actualizan moviéndonos en la dirección que este covector evalúa como la de máximo descenso.

### Figuras

<details>
<summary><b>🖼️ Figura 16.1 — El Gradiente como forma lineal</b></summary>
<br>
<img src="../img/bloque-3/fig-16-1-gradiente-covector.png" width="100%">
<p><em>Líneas de contorno topográficas de una función de coste; el gradiente actúa determinando la densidad de esas líneas, no solo apuntando hacia abajo.</em></p>
</details>
