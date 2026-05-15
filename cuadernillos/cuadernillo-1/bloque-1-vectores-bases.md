# 📐 Cuadernillo I — Bloque I
## El Espacio de los Datos: Vectores y Bases

[⬅️ Volver al Índice Maestro](../README.md)

---

## Capítulo 1: El Axioma de Espacio Vectorial sobre $\mathbb{R}$

### 1.1. Explicación para "Dummies": El lienzo infinito
Imagina una rejilla de píxeles. Un Espacio Vectorial funciona como un reglamento de juego consistente: si sumamos dos dibujos o escalamos uno, el resultado permanece dentro del lienzo.
Garantiza que operaciones con datos (imágenes, sonidos, textos) mantengan su estructura matemática, permitiendo el ajuste de pesos en redes neuronales.
Es la garantía de que podemos operar con la realidad (imágenes, sonidos, textos) sin que la estructura matemática se rompa. Sin este reglamento, no podríamos ni sumar fuerzas en física, ni ajustar pesos en una red neuronal.

### 1.2. Rigor mediante Ejemplo Aplicado: El Espacio de Intensidades 
Cada configuración de imagen es un objeto denominado vectores. Sobre el cuerpo de los reales ($\mathbb{R}$), realizamos dos operaciones críticas:

* **Suma de vectores ($u+v$):** Superposición cerrada de imágenes donde el resultado reside en el mismo espacio de 9 dimensiones.
* **Producto por un escalar ($\lambda \cdot v$):** Ajuste de intensidad o brillo de la imagen mediante un factor real.

Si definimos el sistema sobre el cuerpo de los reales ($\mathbb{R}$), podemos realizar dos operaciones críticas:
* **Suma de vectores ($u+v$):** Superponemos las imágenes. Si el píxel 5 de la imagen A tiene intensidad $x$ y en la imagen B tiene $y$, la imagen resultante tendrá un $x+y$ en ese píxel. La suma debe ser cerrada: el resultado vive en el mismo espacio de 9 dimensiones.
* **Producto por un escalar ($\lambda \cdot v$):** Si multiplicamos la imagen A por $0.5$, estamos reduciendo su brillo a la mitad. Si la multiplicamos por $2.0$, la intensificamos.

**Relación con la IA:**
Cuando una red neuronal "mezcla" información de diferentes neuronas para detectar una forma, está realizando exactamente estas operaciones. Si el sistema no fuera un espacio vectorial, el concepto de "combinación de características" sería imposible.

### 1.3. Matemática Teórica y Justificación
Sea $V$ un conjunto no vacío y $\mathbb{R}$ el cuerpo de reales. $V$ es un espacio vectorial si cumple para todo $u, v, w \in V$ y $\lambda, \mu \in \mathbb{R}$:

* Asociatividad y Conmutatividad de la suma.
* Existencia de elemento neutro ($\vec{0}$) y opuesto.
* Distributividad respecto a suma de vectores y escalares.

**Leyes de Composición Interna (Suma):**
* **Elemento Neutro:** Existe $\vec{0} \in V$ tal que $v + \vec{0} = v$ (La imagen vacía).
* **Elemento Opuesto:** Existe $-v \in V$ tal que $v + (-v) = \vec{0}$ (La imagen que anula el brillo).

**Leyes de Composición Externa (Producto por Escalar):**
* **Distributividad respecto a la suma de vectores:** $\lambda(u + v) = \lambda u + \lambda v$
* **Distributividad respecto a la suma de escalares:** $(\lambda + \mu)v = \lambda v + \mu v$
* **Compatibilidad del producto:** $\lambda(\mu v) = (\lambda\mu)v$
* **Elemento unidad:** $1 \cdot v = v$

**Justificación:**
¿Por qué sobre $\mathbb{R}$? Porque el aprendizaje automático requiere continuidad. Si usáramos números enteros ($\mathbb{Z}$), no podríamos realizar pequeñas correcciones de error (gradientes). El uso de los reales permite que el espacio sea denso, permitiendo que la optimización de la red neuronal sea un viaje suave a través de una superficie infinita de posibilidades.

### 1.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 1.1: El concepto de clausura</b></summary>
  <br>
  <img src="../img/bloque-1/fig-01-1-clausura.png" width="100%">
  <p><em>Un diagrama donde dos rejillas de píxeles (vectores) entran en una caja de suma y sale una tercera rejilla del mismo tamaño.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 1.2: El escalado</b></summary>
  <br>
  <img src="../img/bloque-1/fig-01-2-escalado.png" width="100%">
  <p><em>Una imagen de un número "1" que se desvanece al multiplicarse por $0.5$ y se satura al multiplicarse por $2.0$.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 1.3: Abstracción geométrica</b></summary>
  <br>
  <img src="../img/bloque-1/fig-01-3-suma-geometrica.png" width="100%">
  <p><em>Un plano 2D (representando nuestro espacio 9D) donde se muestra la suma de dos flechas ($u$ y $v$) mediante la regla del paralelogramo, anclando que la suma de imágenes es, en el fondo, una suma de flechas en el hiperespacio.</em></p>
</details>

---

## Capítulo 2: El Píxel como Dimensión ($\mathbb{R}^n$)

### 2.1. Explicación para "Dummies": El mundo de muchas direcciones
Para una IA, cada dato independiente es una nueva dirección. Una foto de 1 megapíxel se visualiza en un espacio de dimensión $n$ con un millón de ejes independientes, permitiendo separar datos complejos.

Si tienes una foto de 1 megapíxel, la IA no ve una superficie plana; ve un espacio con **un millón de direcciones diferentes**. Imagina una habitación donde puedes moverte en un millón de ángulos rectos distintos.

¿Por qué es esto importante? Porque permite que la IA separe cosas que en 2D parecen mezcladas. Es como desenredar un nudo: si solo puedes moverte en un plano, el nudo es imposible; si tienes dimensiones extra, puedes pasar "por encima" de los hilos y deshacerlo.

### 2.2. Rigor mediante Ejemplo Aplicado: De la cuadrícula al vector
Representamos una imagen de 9 píxeles como una tupla donde cada componente es independiente. Los vectores base correspondientes deben ser linealmente independientes.

**El Escenario:**
Cada píxel tiene una identidad única. El píxel de la esquina superior izquierda ($p_1$) no tiene nada que ver con el píxel central ($p_5$). Son **independientes**.

Para representar una imagen, creamos una lista ordenada de 9 números (una tupla). Si el píxel 1 tiene intensidad $0.8$ y el resto están en $0$, nuestro vector es:

$$v = (0.8, 0, 0, 0, 0, 0, 0, 0, 0)$$

**Relación con la IA:**
En los modelos de lenguaje (LLMs), esto se vuelve masivo. Una palabra no se representa por 9 píxeles, sino por un "embedding" de quizás **4096 dimensiones**. Cada dimensión representa un concepto abstracto (género, tiempo, pluralidad, etc.). Entender que cada píxel es una dimensión es el primer paso para entender cómo la IA "entiende" conceptos complejos.

### 2.3. Matemática Teórica y Justificación
Un espacio vectorial $V$ es de dimensión $n$ si posee una base de $n$ vectores. El aprendizaje automático requiere que el espacio sea $\mathbb{R}^n$ para permitir optimizaciones mediante gradientes.

**La Construcción del Espacio $\mathbb{R}^n$:**
Un vector $v$ se define como una secuencia finita de números reales:

$$v = (v_1, v_2, \dots, v_n)$$

Donde cada $v_i$ es la componente del vector en la $i$-ésima dimensión.

**Justificación de la Independencia:**
Para que cada píxel sea realmente una dimensión, los vectores que representan cada posición deben ser **linealmente independientes**. Esto significa que es imposible "fabricar" el brillo del píxel 1 sumando brillos de los otros píxeles. Algebraicamente, si denotamos como $e_i$ al vector base correspondiente al píxel $i$, la única solución para la combinación lineal nula es que todos los coeficientes escalares ($\alpha_i$) sean cero:

$$\alpha_1 e_1 + \alpha_2 e_2 + \dots + \alpha_n e_n = \vec{0} \implies \alpha_1 = \alpha_2 = \dots = \alpha_n = 0$$

Esta independencia es la que garantiza que no perdemos información al aplanar la imagen en un vector. El espacio vectorial $\mathbb{R}^n$ "contiene" todas las imágenes posibles como puntos (o flechas desde el origen) en esta hiper-geometría.

### 2.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 2.1: El "Aplanamiento" (Flattening)</b></summary>
  <br>
  <img src="../img/bloque-1/fig-02-1-flattening.png" width="100%">
  <p><em>Una animación visual donde una matriz $3 \times 3$ se estira para convertirse en un vector columna de $\mathbb{R}^9$.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 2.2: Proyección 2D vs 3D</b></summary>
  <br>
  <img src="../img/bloque-1/fig-02-2-proyeccion-2d-3d.png" width="100%">
  <p><em>Una analogía visual que muestre cómo dos puntos que parecen estar uno encima del otro en 2D se separan claramente cuando añadimos una tercera dimensión (eje $Z$).</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 2.3: El Hiperespacio</b></summary>
  <br>
  <img src="../img/bloque-1/fig-02-3-hiperespacio.png" width="100%">
  <p><em>Un sistema de coordenadas con 3 ejes ($X, Y, Z$) donde cada eje está etiquetado con la posición de un píxel, mostrando un vector como un punto único en ese espacio.</em></p>
</details>

---

## Capítulo 3: Independencia Lineal: La pureza de la información

### 3.1. Explicación para "Dummies": El mensajero que no aporta nada
La Independencia Lineal garantiza que cada neurona aporta información única. Si un dato puede deducirse de otros, es redundante y se considera linealmente dependiente.

En una red neuronal, la **Independencia Lineal** es la garantía de que cada píxel (o cada neurona) nos está diciendo algo nuevo. Si un píxel se puede "adivinar" sumando o restando otros píxeles, ese píxel es **dependiente**. Es ruido, es redundancia. La IA busca la "información pura", y para eso necesita que sus "mensajeros" (vectores) sean independientes.

### 3.2. Rigor mediante Ejemplo Aplicado: La redundancia en la rejilla
Supongamos que en nuestra rejilla de $3 \times 3$, por un fallo de la cámara, el píxel 3 ($p_3$) siempre tiene exactamente la suma del brillo del píxel 1 ($p_1$) y el píxel 2 ($p_2$).

**El Escenario:**
Aquí, el vector $e_3$ es **linealmente dependiente** de $e_1$ y $e_2$.

**Relación con la IA:**
Cuando entrenamos una red, si tenemos muchas variables que dicen lo mismo (correlación perfecta), la red se vuelve inestable o ineficiente. El proceso de "limpiar" datos o de usar capas de compresión busca, en esencia, eliminar esta dependencia para quedarse solo con la base que genera la información real.

### 3.3. Matemática Teórica y Justificación
Sea $S = \{v_1, v_2, \dots, v_k\}$ un conjunto de vectores en el espacio vectorial $V$. Decimos que estos vectores son **Linealmente Independientes** (L.I.) si la única combinación lineal que da como resultado el vector nulo es la que tiene todos sus coeficientes iguales a cero:

$$\alpha_1 v_1 + \alpha_2 v_2 + \dots + \alpha_k v_k = \vec{0} \implies \alpha_1 = \alpha_2 = \dots = \alpha_k = 0$$

**Justificación:**
Si existe algún $\alpha_i \neq 0$, significa que podemos expresar uno de los vectores como combinación de los otros (dependencia).
En el contexto de las redes neuronales, la independencia lineal está ligada al **Rango** de las matrices de pesos. Si las filas de una matriz de una capa son dependientes, la red está "colapsando" dimensiones, perdiendo capacidad de aprendizaje. La independencia es lo que nos asegura que el espacio donde opera la IA tiene la dimensión máxima posible para resolver el problema.

### 3.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 3.1: Vectores en la misma línea</b></summary>
  <br>
  <img src="../img/bloque-1/fig-03-1-dependencia.png" width="100%">
  <p><em>Dos flechas sobrepuestas (dependientes) vs. dos flechas en distintas direcciones (independientes) en un plano.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 3.2: El concepto de "Sombra"</b></summary>
  <br>
  <img src="../img/bloque-1/fig-03-2-sombra.png" width="100%">
  <p><em>Un vector que cae dentro del plano generado por otros dos, mostrando visualmente que no aporta una "nueva altura" al espacio.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 3.3: Redundancia de Píxeles</b></summary>
  <br>
  <img src="../img/bloque-1/fig-03-3-redundancia.png" width="100%">
  <p><em>Una imagen donde dos píxeles siempre se iluminan igual, comparada con una donde son independientes, marcando la primera como "Información Redundante".</em></p>
</details>

---

## Capítulo 4: Sistemas de Generadores y el concepto de Base

### 4.1. Explicación para "Dummies": El kit de construcción definitivo
Si con un conjunto de piezas puedes construir cualquier objeto del espacio, tienes un Sistema de Generadores. Si además el conjunto es el mínimo necesario, constituye una Base.
Si, además, te han dado exactamente las piezas necesarias (ni un tornillo de más ni uno de menos), entonces tienes una **Base**.

En la IA, una base son los "átomos" mínimos de información. Si tienes una base de 9 píxeles, puedes construir cualquier imagen de 9 píxeles. Si te falta uno, hay imágenes que nunca podrás representar. Si te sobra uno, tienes desorden. La base es el equilibrio perfecto entre posibilidad y eficiencia.

### 4.2. Rigor mediante Ejemplo Aplicado: Los 9 átomos del "1"
Volvemos a nuestra rejilla de $3 \times 3$. Para poder "dibujar" cualquier cosa en ella, necesitamos 9 vectores fundamentales.

**El Escenario:**
Definimos los vectores $\{e_1, \dots, e_9\}$, donde cada $e_i$ es una imagen con un solo píxel encendido al $100\%$.
Cualquier imagen de número que escribas, como un "1", no es más que una **receta** (combinación lineal) de estos 9 vectores.

Si el "1" usa los píxeles 2, 5 y 8, la receta es:

$$v = 1 \cdot e_2 + 1 \cdot e_5 + 1 \cdot e_8$$

**Relación con la IA:**
En el procesamiento de lenguaje natural (NLP), esto es fascinante. No usamos píxeles, usamos "conceptos base". Si tu base conceptual es pobre, tu IA no podrá generar ideas complejas. La **dimensión de la base** determina la "riqueza" de lo que la IA puede llegar a comprender o crear.

### 4.3. Matemática Teórica y Justificación
Sea $V$ un espacio vectorial. Un conjunto de vectores $S = \{v_1, \dots, v_k\}$ es un **Sistema de Generadores** de $V$ si todo vector $v \in V$ puede expresarse como una combinación lineal de ellos:

$$v = \alpha_1 v_1 + \alpha_2 v_2 + \dots + \alpha_k v_k$$

Un conjunto $B$ es una **Base** de $V$ si cumple dos condiciones simultáneamente:
1. Es un sistema de generadores (Cubre todo el espacio).
2. Es linealmente independiente (No hay piezas redundantes).

**Justificación:**
El concepto de base es lo que permite introducir las **coordenadas**. Si $B$ es una base, los escalares $\alpha_i$ para representar cualquier vector son **únicos**.
En ingeniería de IA, esto es vital: si la representación no fuera única, el proceso de aprendizaje (ajuste de pesos) sería caótico, porque habría infinitas formas de representar el mismo dato. La base garantiza que cada imagen tenga un "DNI" numérico irrepetible en ese espacio.

### 4.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 4.1: Los 9 Vectores Canónicos</b></summary>
  <br>
  <img src="../img/bloque-1/fig-04-1-vectores-canonicos.png" width="100%">
  <p><em>Una cuadrícula de 9 pequeñas imágenes, cada una con un solo píxel blanco, etiquetadas de $e_1$ a $e_9$.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 4.2: La Receta del Dígito</b></summary>
  <br>
  <img src="../img/bloque-1/fig-04-2-receta-digito.png" width="100%">
  <p><em>Un diagrama donde el número "1" se descompone en la suma de tres de esos vectores base multiplicados por sus respectivos pesos (intensidades).</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 4.3: El Espacio Generado (Span)</b></summary>
  <br>
  <img src="../img/bloque-1/fig-04-3-span.png" width="100%">
  <p><em>Una visualización 3D donde dos vectores base definen un plano (el espacio de todas las imágenes posibles de 2 píxeles), mostrando que fuera de ese plano "no existe" nada para ese sistema.</em></p>
</details>

---

## Capítulo 5: Coordenadas y el Vector como combinación lineal

### 5.1. Explicación para "Dummies": El GPS del Hiperespacio
Las coordenadas son la "receta" numérica que indica cuánto desplazarse en cada dirección de la base para representar un dato específico.

Imagina que quieres explicarle a alguien cómo hacer tu café exacto. No le das el café; le das la "receta": 2 de agua, 1 de café, 0.5 de azúcar. Esos números (2, 1, 0.5) son las coordenadas. Si cambias el orden o los números, el resultado es otro café.

En la IA, cuando decimos que una imagen es un vector de números, estamos dando la **receta de intensidades** para que la pantalla sepa exactamente cuánto brillo poner en cada dirección de la base.

### 5.2. Rigor mediante Ejemplo Aplicado: La receta del "1" imperfecto
Retomamos nuestra base canónica $B = \{e_1, \dots, e_9\}$ de la rejilla $3 \times 3$.

**El Escenario:**
Queremos representar un número "1" que no es perfecto. El centro tiene intensidad máxima, pero arriba y abajo el trazo es más débil.
* Instrucción 1: En la dirección $e_2$ (arriba centro), pon $0.6$.
* Instrucción 2: En la dirección $e_5$ (centro), pon $1.0$.
* Instrucción 3: En la dirección $e_8$ (abajo centro), pon $0.6$.

El vector resultante $v$ se escribe como una **Combinación Lineal**:

$$v = 0.6 e_2 + 1.0 e_5 + 0.6 e_8$$

**Relación con la IA:**
Cuando una red neuronal procesa una imagen, las "activaciones" de las capas ocultas son coordenadas en un espacio de conceptos. Si una neurona detecta "curvatura" y otra "linealidad", el vector de esa capa nos dice cuánto de cada concepto tiene el objeto. Los **pesos** de la red son, en esencia, los que deciden cómo se mezclan estas coordenadas para pasar a la siguiente etapa.

### 5.3. Matemática Teórica y Justificación
Sea $V$ un espacio vectorial de dimensión $n$ y $B$ una base de $V$. Para cualquier vector $v \in V$, existe una **única** combinación de escalares $\alpha_i$ tal que:

$$v = \alpha_1 b_1 + \alpha_2 b_2 + \dots + \alpha_n b_n$$

A estos escalares se les denomina **coordenadas** de $v$ respecto a la base $B$.

**Justificación de la Unicidad:**
La unicidad es la propiedad más potente de una base. Si pudiéramos representar un vector con dos recetas distintas bajo la misma base, la IA nunca podría aprender, porque no habría una relación unívoca entre el dato y su representación. Al ser $B$ linealmente independiente, se garantiza que:

$$\sum_{i=1}^{n} \alpha_i b_i = \sum_{i=1}^{n} \beta_i b_i \implies \alpha_i = \beta_i \quad \forall i$$

Esto nos permite tratar a los vectores como columnas de números (vectores de $\mathbb{R}^n$) sin perder ni un ápice de información geométrica. Es lo que permite que el software (que solo entiende números) maneje la geometría (que entiende formas).

### 5.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 5.1: La Suma Ponderada</b></summary>
  <br>
  <img src="../img/bloque-1/fig-05-1-suma-ponderada.png" width="100%">
  <p><em>Visualización de cómo tres vectores base, multiplicados por diferentes transparencias (escalares), se fusionan para crear el vector final.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 5.2: Unicidad del Punto</b></summary>
  <br>
  <img src="../img/bloque-1/fig-05-2-unicidad.png" width="100%">
  <p><em>Un punto en un espacio 3D con líneas de proyección hacia los ejes, mostrando que solo hay un conjunto de valores $(\alpha_1, \alpha_2, \alpha_3)$ que lo definen.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 5.3: El Vector de Activación</b></summary>
  <br>
  <img src="../img/bloque-1/fig-05-3-activacion.png" width="100%">
  <p><em>Una representación de una neurona recibiendo múltiples señales (coordenadas) y sumándolas para generar una salida.</em></p>
</details>

---

## Capítulo 6: Subespacios Vectoriales

### 6.1. Explicación para "Dummies": La habitación dentro del palacio
Imagina que vives en un palacio con un millón de habitaciones (dimensiones), pero tú solo te mueves entre la cocina, el dormitorio y el baño. Aunque el palacio es inmenso, tu vida ocurre en un **subespacio** de ese palacio.

Un Subespacio Vectorial es una región del espacio total que mantiene las mismas reglas algebraicas. En IA, los datos útiles suelen residir en subespacios de menor dimensión.

### 6.2. Rigor mediante Ejemplo Aplicado: El Subespacio de las "Líneas Horizontales"
Volvamos a nuestra rejilla de $3 \times 3$ ($\mathbb{R}^9$). Supongamos que estamos entrenando a una IA para que detecte solo trazos horizontales en la parte superior.

**El Escenario:**
Solo nos interesan los píxeles de la primera fila: $\{e_1, e_2, e_3\}$.
Cualquier imagen que sea una combinación lineal de estos tres (y solo estos tres) pertenece al **Subespacio de la Fila Superior ($S$)**.
* Si sumas dos imágenes que solo tienen píxeles arriba, el resultado sigue teniendo píxeles solo arriba.
* Si haces más brillante una imagen "de arriba", no aparecen píxeles mágicamente en la fila de abajo.

**Relación con la IA:**
Esto es lo que ocurre en las **Capas de Compresión** (como en los Autoencoders). La IA intenta proyectar una imagen compleja de 784 píxeles en un subespacio de, digamos, 32 dimensiones (el "Latent Space"). La IA aprende que los datos reales viven en un subespacio mucho más pequeño que el espacio total de píxeles posibles. Si logramos encontrar el subespacio correcto, la IA procesa la información miles de veces más rápido.

### 6.3. Matemática Teórica y Justificación
Sea $V$ un espacio vectorial sobre $\mathbb{R}$. Un subconjunto no vacío $S$ es un **Subespacio Vectorial** de $V$ si y solo si es, por sí mismo, un espacio vectorial con las mismas operaciones de $V$.
Para verificarlo, usamos el **Teorema de Caracterización de Subespacios**, que exige cumplir dos condiciones de clausura:
1.  **Clausura bajo la suma:** $u, v \in S \implies u + v \in S$.
2.  **Clausura bajo el producto escalar:** $v \in S, \lambda \in \mathbb{R} \implies \lambda v \in S$.

*Nota: Todo subespacio debe contener obligatoriamente al vector nulo ($\vec{0}$).*

**Justificación:**
¿Por qué nos importa que sea un subespacio y no solo un "grupo de vectores"? Porque la estructura de subespacio nos permite aplicar todas las herramientas del álgebra lineal (bases, proyecciones, transformaciones) dentro de esa región. En IA, esto garantiza que las manipulaciones que hagamos sobre los datos comprimidos (embeddings) sigan siendo consistentes y no generen "basura" matemática que la red no sepa interpretar.

### 6.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 6.1: El Plano en el Espacio</b></summary>
  <br>
  <img src="../img/bloque-1/fig-06-1-plano-espacio.png" width="100%">
  <p><em>Un espacio 3D con un plano coloreado que lo atraviesa por el origen. Muestra vectores sumándose dentro del plano y sin poder "escapar" de él.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 6.2: El Filtro de Fila</b></summary>
  <br>
  <img src="../img/bloque-1/fig-06-2-filtro-fila.png" width="100%">
  <p><em>Una rejilla de $3 \times 3$ donde solo se iluminan los píxeles de la fila superior, comparada con una donde se iluminan otros, marcando la primera como miembro del subespacio.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 6.3: Compresión Latente</b></summary>
  <br>
  <img src="../img/bloque-1/fig-06-3-compresion-latente.png" width="100%">
  <p><em>Un embudo que toma un vector grande y lo proyecta sobre un subespacio de menor dimensión.</em></p>
</details>
