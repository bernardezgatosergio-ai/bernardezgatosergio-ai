# 📐 Cuadernillo I — Bloque III
## La Evaluación del Dato: El Espacio Dual y Covectores

> *"Un vector es una flecha en el espacio. Un covector es la regla graduada que mide esa flecha."*

[⬅️ Volver al Índice Maestro](../README.md)

---

## Capítulo 12: El concepto de Funcional Lineal: El mapeo de la decisión

### 12.1. Explicación para "Dummies": La Máquina de un solo número
Un Funcional Lineal es una aplicación que reduce un vector complejo a un único número escalar evaluativo.

No es una máquina que transforma la foto en otra foto; es una máquina que la evalúa.
Una máquina podría decirte: "¿Cuánta resina tiene?" -> Resultado: $0.85$.
Otra podría decir: "¿Es un nudo de madera?" -> Resultado: $1$ (muy probable).

En la IA, cada neurona de la primera capa es una de estas máquinas. Su único trabajo es mirar el espacio de entrada y "reducirlo" a un escalar que resuma una característica.

### 12.2. Rigor mediante Ejemplo Aplicado: El Detector de "Brillo Superior"
Volvemos a nuestra rejilla de $3 \times 3$. Queremos diseñar una neurona (funcional) que solo se preocupe por cuánto brillo hay en la fila de arriba, ignorando el resto.

**El Escenario:**
Definimos nuestro funcional $f$. Si le pasamos una imagen $v$, el funcional hace lo siguiente:
* Mira el píxel 1, 2 y 3.
* Los suma.
* Ignora los píxeles 4 al 9.

Si entra una imagen con la fila superior iluminada, el resultado es alto.
Si entra una imagen con mucho brillo abajo pero nada arriba, el resultado es $0$.

**Relación con la IA:**
Aquí es donde el alumno entiende la Neurona Artificial. Una neurona no es un objeto estático; es una función que mapea un espacio de alta dimensión (píxeles) a un espacio de una dimensión ($\mathbb{R}$). Lo que llamamos "entrenar la neurona" es en realidad ajustar este funcional para que el número que escupa sea útil para la clasificación.

### 12.3. Matemática Teórica y Justificación
Sea $V$ un espacio vectorial sobre $\mathbb{R}$. Un Funcional Lineal es una aplicación $f: V \to \mathbb{R}$ que satisface la propiedad de linealidad para todo $u, v \in V$ y $\lambda \in \mathbb{R}$:
* **Aditividad:** $f(u + v) = f(u) + f(v)$
* **Homogeneidad:** $f(\lambda v) = \lambda f(v)$

**Justificación:**
¿Por qué la linealidad es innegociable aquí?
* **Proporcionalidad:** Si una imagen tiene el doble de brillo, la respuesta de la neurona debe ser el doble (antes de pasar por la activación no lineal).
* **Superposición:** La respuesta de la neurona a dos formas superpuestas debe ser la suma de las respuestas a cada forma por separado.

Este mapeo de $\mathbb{R}^n \to \mathbb{R}$ es una operación de compresión extrema. Estamos perdiendo casi toda la información del vector para quedarnos con un solo dato escalar. El conjunto de todos estos posibles funcionales es tan vasto y está tan bien estructurado que forma su propio espacio, el cual estudiaremos en el siguiente capítulo.

### 12.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 12.1: El Embudo Escalar</b></summary>
  <br>
  <img src="../img/bloque-3/fig-12-1-embudo.png" width="100%">
  <p><em>Un vector grande (rejilla 3x3) entrando en una caja etiquetada como "$f$" y saliendo de ella un único número real sobre una recta numérica.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 12.2: La Selección de Características</b></summary>
  <br>
  <img src="../img/bloque-3/fig-12-2-seleccion.png" width="100%">
  <p><em>Un esquema que muestra cómo el funcional "pesa" ciertos píxeles y pone a cero otros, actuando como un filtro que extrae una sola propiedad.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 12.3: Linealidad de la Evaluación</b></summary>
  <br>
  <img src="../img/bloque-3/fig-12-3-linealidad.png" width="100%">
  <p><em>Dos imágenes sumándose antes de entrar al funcional, y el resultado siendo igual a la suma de las imágenes evaluadas por separado: $f(u + v) = f(u) + f(v)$.</em></p>
</details>

---

## Capítulo 13: El Espacio Dual $V^*$: El universo de los parámetros

### 13.1. Explicación para "Dummies": El catálogo de lupas
El Espacio Dual $V^*$ es el conjunto de todos los funcionales posibles. Cada neurona es un habitante de este espacio.

Esa caja de lupas es el Espacio Dual $V^*$. Cada "lupa" (funcional) es un habitante de este espacio. 
No son sellos. 
Son herramientas que actúan sobre los sellos para darnos un dato.

En una red neuronal, cuando ves una capa con 512 neuronas, lo que tienes es un espacio dual de dimensión 512. Cada neurona es una "lupa" distinta que está mirando el mismo dato de entrada para extraer una conclusión diferente.

### 13.2. Rigor mediante Ejemplo Aplicado: Los pesos de la neurona
Volvemos a nuestra rejilla de $3 \times 3$. Tenemos una imagen $v$ (un vector de 9 números).

**El Escenario:**
Para procesar esa imagen, definimos un conjunto de pesos (weights). Supongamos que queremos detectar si hay un trazo horizontal en medio. Definimos un elemento del espacio dual, llamémoslo $w$, mediante sus coeficientes:

$$w = [0, 0, 0, 1, 1, 1, 0, 0, 0]$$

Cuando este funcional $w$ actúa sobre cualquier imagen $v$, realiza la operación:

$$w(v) = 0 \cdot v_1 + \dots + 1 \cdot v_4 + 1 \cdot v_5 + 1 \cdot v_6 + \dots = v_4 + v_5 + v_6$$

**Relación con la IA:**
Aquí está el secreto mejor guardado: Los pesos de una neurona no son un vector del espacio original, son un vector del espacio dual.
* $v \in V$ (El dato).
* $w \in V^*$ (El parámetro).

El entrenamiento (Backpropagation) no consiste en cambiar el dato, sino en movernos por el espacio dual hasta encontrar la "lupa" (los pesos) que mejor clasifica la realidad.

### 13.3. Matemática Teórica y Justificación
Sea $V$ un espacio vectorial sobre $\mathbb{R}$. Definimos el Espacio Dual $V^*$ como el conjunto de todos los funcionales lineales $f: V \to \mathbb{R}$.

**Propiedades Estructurales:**
* **Espacio Vectorial:** $V^*$ es en sí mismo un espacio vectorial. Podemos sumar dos funcionales (dos formas de medir) y obtener una nueva, o multiplicar un funcional por un escalar (darle más o menos importancia).
* **Dimensión:** Si $V$ tiene dimensión finita $n$, entonces $V^*$ también tiene dimensión $n$.
* **Dualidad:** A los elementos de $V$ los llamamos vectores (o vectores contravariantes) y a los de $V^*$ los llamamos covectores (o vectores covariantes).

**Justificación:**
¿Por qué separar ambos espacios si tienen la misma dimensión? Porque se comportan de forma distinta ante cambios de escala. Si decides medir tus píxeles en una escala del 1 al 100 en lugar de 0 a 1 (estiras el espacio $V$), los pesos de tu neurona ($V^*$) deben encogerse proporcionalmente para que el resultado final sea el mismo. Esta relación inversa es la que define la covarianza, fundamental para entender cómo escalan los modelos de IA en producción.

### 13.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 13.1: El Producto Interno como Interacción</b></summary>
  <br>
  <img src="../img/bloque-3/fig-13-1-interaccion.png" width="100%">
  <p><em>Un vector columna (dato) encontrándose con un vector fila (pesos). La interacción produce un escalar. Es la visualización de la dualidad.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 13.2: El Espacio de las Reglas</b></summary>
  <br>
  <img src="../img/bloque-3/fig-13-2-reglas.png" width="100%">
  <p><em>Un plano que representa $V$ con puntos (datos) y un espacio paralelo que representa $V^*$ con planos de nivel que "rebanan" el espacio original.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 13.3: Dualidad en la Neurona</b></summary>
  <br>
  <img src="../img/bloque-3/fig-13-3-neurona.png" width="100%">
  <p><em>El esquema clásico de una neurona, pero etiquetando claramente los inputs como pertenecientes a $V$ y los pesos como pertenecientes a $V^*$.</em></p>
</details>

---

## Capítulo 14: El concepto de Hiperplano: Separando la realidad matemáticamente

### 14.1. Explicación para "Dummies": El muro de cristal
Un Hiperplano Afín es la frontera de decisión que divide el espacio en dos categorías.

Si las canicas estuvieran flotando en una habitación (3D), necesitarías una hoja de papel infinita para separarlas. Eso es un hiperplano en 3D.
¿Y si las canicas tienen 1.000 dimensiones (como los píxeles de una imagen)? Sigues necesitando un "muro", pero un muro de 999 dimensiones. El Hiperplano es el corte perfecto que divide el universo en dos: "Lo que es A" y "Lo que no es A".

### 14.2. Rigor mediante Ejemplo Aplicado: Separación de maderas
Supongamos que medimos dos características de una pieza de madera: Densidad ($x_1$) y Resistencia al corte ($x_2$).

**El Escenario:**
Queremos que nuestra IA decida si la madera es "Roble" (Clase $1$) o "Pino" (Clase $0$). Tras el entrenamiento, la IA ha encontrado un funcional en el espacio dual cuyos pesos son $w = [w_1, w_2]$ y un umbral de decisión (sesgo) $b$.

La frontera de decisión es el conjunto de puntos donde:

$$w_1 x_1 + w_2 x_2 + b = 0$$

Si el resultado es $> 0$, la IA predice Roble.
Si el resultado es $< 0$, la IA predice Pino.

**Relación con la IA:**
Este es el fundamento de las Máquinas de Vector de Soporte (SVM) y de la capa de salida de casi cualquier red neuronal. El hiperplano es la "sentencia" del modelo. Entrenar una IA es, en esencia, mover ese muro por el hiperespacio hasta que deje a todos los "perros" a un lado y a todos los "gatos" al otro con el mayor margen posible.

### 14.3. Matemática Teórica y Justificación
Sea $V$ un espacio vectorial de dimensión $n$. Un Hiperplano Afín $H$ es un subespacio de dimensión $n-1$ trasladado. Matemáticamente, se define a través de un funcional lineal no nulo $f \in V^*$ y un escalar $b \in \mathbb{R}$:

$$H = \{ v \in V \mid f(v) + b = 0 \}$$

**Propiedades Críticas:**
* **Vector Normal:** El funcional $f$ define la dirección perpendicular al hiperplano. En un espacio euclídeo, esto corresponde al vector de pesos $w$.
* **Partición del Espacio:** Un hiperplano divide al espacio $V$ en dos semi-espacios abiertos: $f(v) + b > 0$ y $f(v) + b < 0$.
* **Kernel:** Si $b = 0$, el hiperplano es exactamente el Núcleo (Kernel) del funcional lineal, es decir, el lugar donde el funcional se anula.

**Justificación:**
¿Por qué es tan importante que sea lineal? Porque la linealidad garantiza que la frontera sea "plana". Si permitiéramos fronteras curvas sin control, el modelo sufriría de overfitting (memorizaría los datos en lugar de aprender). El hiperplano es la forma más simple y robusta de generalizar una decisión en alta dimensión.

### 14.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 14.1: La Frontera en 2D</b></summary>
  <br>
  <img src="../img/bloque-3/fig-14-1-frontera-2d.png" width="100%">
  <p><em>Dos nubes de puntos claramente separadas por una línea recta. Se marcan los vectores que están justo en el borde (vectores de soporte).</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 14.2: Proyección del Hiperplano en 3D</b></summary>
  <br>
  <img src="../img/bloque-3/fig-14-2-hiperplano-3d.png" width="100%">
  <p><em>Un plano atravesando un cubo de datos, dividiendo el volumen en dos regiones de colores distintos.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 14.3: El Vector Normal (Covector)</b></summary>
  <br>
  <img src="../img/bloque-3/fig-14-3-vector-normal.png" width="100%">
  <p><em>El plano de decisión y una flecha (el covector del espacio dual) saliendo de él a $90^\circ$, mostrando que el funcional es quien "manda" sobre la orientación del muro.</em></p>
</details>

---

## Capítulo 15: La Base Dual y la Delta de Kronecker: El detector de píxeles puro

### 15.1. Explicación para "Dummies": La mesa de mezclas perfecta
La Base Dual permite el aislamiento total de canales de información mediante la Delta de Kronecker.

Una Base Dual es la configuración perfecta de esa mesa de mezclas, donde el deslizador 1 controla única y exclusivamente el volumen del canal 1, sin afectar lo más mínimo a los canales 2 al 9. El deslizador 2 controla solo el canal 2, y así sucesivamente.

Parece obvio, pero matemáticamente requiere una construcción específica. La Delta de Kronecker es el interruptor que garantiza este comportamiento: "Si el deslizador $\phi_i$ actúa sobre el canal $e_j$, el resultado es $1$ si $i=j$ (son el mismo canal) y $0$ si $i \neq j$ (son canales distintos)". Es el aislamiento total de la información.

### 15.2. Rigor mediante Ejemplo Aplicado: El Filtro de Píxel Único
Volvemos a nuestra rejilla de $3 \times 3$ con su base canónica $B = \{e_1, \dots, e_9\}$. Recuerda que $e_5$ es una imagen donde solo el píxel central está encendido.

**El Escenario:**
Queremos diseñar una neurona (un funcional en $V^*$), llamémoslo $\phi_5$, cuyo único objetivo sea medir la intensidad del píxel central. Ignorando completamente los otros 8 píxeles.

Si le pasamos la imagen $e_5$, queremos que el resultado sea $1$ (detección perfecta).
Si le pasamos la imagen $e_1$ (píxel esquina encendido), queremos que el resultado sea $0$.

El funcional $\phi_5$ se define por un conjunto de pesos. Para que funcione como queremos, sus pesos deben ser $[0, 0, 0, 0, 1, 0, 0, 0, 0]$. Al actuar sobre $e_5$:

$$\phi_5(e_5) = 0 \cdot 0 + \dots + 1 \cdot 1 + \dots = 1$$

Al actuar sobre $e_1$:

$$\phi_5(e_1) = 0 \cdot 1 + \dots + 1 \cdot 0 + \dots = 0$$

**Relación con la IA:**
Este funcional $\phi_5$ es un elemento de la Base Dual. En IA, esto es fundamental para el Indexing (indexación) y la extracción de características puras. Antes de que una red compleja mezcle píxeles (convoluciones), necesitamos la capacidad matemática de referirnos a "la intensidad del píxel (2,2)" de forma aislada. La base dual provee esos "sensores puros".

### 15.3. Matemática Teórica y Justificación
Sea $V$ un espacio vectorial de dimensión finita $n$, y sea $B = \{e_1, \dots, e_n\}$ una base de $V$. Existe una única base de $V^*$, denotada por $B^* = \{\phi^1, \dots, \phi^n\}$, llamada la Base Dual de $V$.

Los elementos de $B^*$ se definen por su acción sobre los elementos de $B$ mediante la Delta de Kronecker ($\delta_j^i$):

$$\phi^i(e_j) = \delta_j^i = \begin{cases} 1 & \text{si } i = j \\ 0 & \text{si } i \neq j \end{cases}$$

*(Nota de notación: Usamos superíndices para los covectores de la base dual para facilitar la notación de Einstein que veremos más adelante).*

**Justificación:**
* **Demostración de Dimensión:** La existencia de esta base dual prueba rigurosamente que $\dim(V) = \dim(V^*)$.
* **Representación de Coordenadas:** Cualquier funcional lineal $f$ puede escribirse como una combinación lineal de la base dual: $f = \sum_{i=1}^n c_i \phi^i$. Y lo más potente: las coordenadas $c_i$ son simplemente el funcional evaluado en los vectores de la base original, $c_i = f(e_i)$.
* **Backpropagation:** Esta relación uno-a-uno es la que permite que, durante el entrenamiento, cuando calculamos el error en una neurona de salida, sepamos exactamente qué peso específico ajustar en relación con qué entrada específica. La Delta de Kronecker es el "mapa de cableado" que hace posible el aprendizaje supervisado.

### 15.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 15.1: La Delta de Kronecker Visual</b></summary>
  <br>
  <img src="../img/bloque-3/fig-15-1-kronecker.png" width="100%">
  <p><em>Una matriz de 3x3 rejillas de píxeles. El eje Y representa el covector aplicado ($\phi^i$) y el eje X el vector de entrada ($e_j$). Solo la diagonal principal de la matriz está iluminada (resultado $1$), el resto está oscuro (resultado $0$).</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 15.2: El "Cableado" de la Base Dual</b></summary>
  <br>
  <img src="../img/bloque-3/fig-15-2-cableado.png" width="100%">
  <p><em>Un diagrama con 3 neuronas de entrada y 3 neuronas de salida que representan la base dual. Líneas directas conectan canales aislados mostrando el aislamiento.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 15.3: Notación de Índices (Contravariante vs Covariante)</b></summary>
  <br>
  <img src="../img/bloque-3/fig-15-3-indices.png" width="100%">
  <p><em>Un diagrama tipográfico que resalta el índice inferior y el superior, mostrando cómo se "cancelan" mediante la delta de Kronecker $\phi^i(e_j) = \delta_j^i$.</em></p>
</details>

---

## Capítulo 16: Isomorfismos Naturales y el Teorema de Representación de Riesz

### 16.1. Explicación para "Dummies": El "Objeto Prototipo"
El Teorema de Representación de Riesz establece que cada funcional tiene un vector gemelo que permite representarlo mediante un producto escalar.

El Teorema de Riesz dice exactamente eso: en espacios donde podemos medir distancias (espacios euclídeos), toda regla de evaluación (funcional) tiene un vector "gemelo" en el espacio original que hace exactamente el mismo trabajo mediante un producto escalar.

Por eso, cuando ves los pesos de una red convolucional, los ves como "filtros" o imágenes pequeñas. Estamos usando el vector prototipo para representar la regla de detección.

### 16.2. Rigor mediante Ejemplo Aplicado: Visualización de Pesos
Supongamos una red neuronal que clasifica dígitos. La primera neurona debe detectar la línea vertical del número "1".

**El Escenario:**
Técnicamente, la neurona es un funcional $f \in V^*$. Pero gracias a Riesz, podemos encontrar un vector $v_f \in V$ tal que la activación sea $f(x) = \langle x, v_f \rangle$.

Si $v_f$ tiene esta forma:
$[0, 1, 0, 0, 1, 0, 0, 1, 0]$ (visto como imagen).

Cualquier imagen de entrada $x$ que se parezca a ese "prototipo" dará un resultado alto. Hemos convertido una operación abstracta en una comparación visual.

**Relación con la IA:**
Esta es la razón por la que en el análisis de interpretabilidad de modelos (como LIME o SHAP), podemos dibujar "mapas de calor" sobre la imagen original. Estamos proyectando los pesos del Dual de vuelta al espacio de los Píxeles para que un humano pueda entender qué está "mirando" la máquina. Sin este isomorfismo, los pesos serían solo una lista de números sin significado geométrico.

### 16.3. Matemática Teórica y Justificación
Sea $V$ un espacio vectorial de dimensión finita con un producto escalar $\langle \cdot, \cdot \rangle$. El Teorema de Representación de Riesz establece que para cada funcional lineal $f \in V^*$, existe un único vector $v_f \in V$ tal que:

$$f(x) = \langle x, v_f \rangle \quad \forall x \in V$$

**Consecuencias Matemáticas:**
* **Isomorfismo Natural:** La aplicación $\Phi: V \to V^*$ que envía cada vector $v$ al funcional $\langle \cdot, v \rangle$ es un isomorfismo. Esto significa que $V$ y $V^*$ son estructuralmente idénticos mientras el producto escalar no cambie.
* **Identificación de Bases:** Si la base $B=\{e_i\}$ es ortonormal, entonces su base dual $B^*$ se identifica directamente con los mismos vectores: $\phi^i \equiv e_i$.
* **El peligro de la comodidad:** Muchos desarrolladores de IA olvidan que esta identificación depende del producto escalar. Si cambias la métrica del espacio (por ejemplo, usando una norma distinta), el "vector prototipo" cambia, pero el funcional original (la regla) sigue siendo el mismo.

**Justificación:**
Este teorema es el que permite que el Descenso de Gradiente funcione. El gradiente es, por definición, un elemento del Dual (indica cómo cambia una función), pero lo restamos directamente de los pesos (que tratamos como vectores) porque Riesz nos permite identificarlos en el mismo espacio.

### 16.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 16.1: El Espejo de Riesz</b></summary>
  <br>
  <img src="../img/bloque-3/fig-16-1-espejo.png" width="100%">
  <p><em>Un diagrama con dos planos paralelos ($V$ y $V^*$). Una flecha de doble sentido conecta un funcional con su vector representante, mediado por el símbolo del producto escalar.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 16.2: Filtros de Convolución como Vectores</b></summary>
  <br>
  <img src="../img/bloque-3/fig-16-2-convolucion.png" width="100%">
  <p><em>Una red neuronal mostrando una capa oculta. Se hace zoom en una neurona para mostrar que sus "pesos" forman una pequeña imagen que busca patrones.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 16.3: El Colapso de la Dualidad</b></summary>
  <br>
  <img src="../img/bloque-3/fig-16-3-colapso.png" width="100%">
  <p><em>Una animación conceptual donde el vector fila (Dual) y el vector columna (Espacio) se funden en un solo objeto gracias a la métrica euclídea.</em></p>
</details>
