# 📐 Cuadernillo I — Bloque IV
## Aplicaciones Lineales y Factorización Matricial

[⬅️ Volver al Índice Maestro](../README.md)

---

## Capítulo 17: La Aplicación Lineal: La transformación del dato entre capas

### 17.1. Explicación para "Dummies": El Traductor de Mundos
Una Aplicación Lineal transporta vectores entre espacios manteniendo la linealidad de la información.

En una red neuronal, cada capa es una aplicación lineal. El dato entra como una lista de píxeles y sale como una lista de "conceptos". La aplicación lineal es el puente que traduce el lenguaje de la entrada al lenguaje de la siguiente capa. Si el puente es malo, la información se pierde; si es bueno, la IA empieza a comprender patrones.

### 17.2. Rigor mediante Ejemplo Aplicado: La Capa Densa
Supongamos que tenemos una capa de entrada con 3 neuronas (nuestra rejilla simplificada) y queremos pasar a una capa oculta con 2 neuronas que detectan "formas".

**El Escenario:**
Tenemos un vector de entrada $x$. La aplicación lineal $T$ va a transformar este vector en uno nuevo $y$.

Para que esta transformación ocurra, cada neurona de la salida debe ser una combinación de las entradas. Por ejemplo:

$$y_1 = w_{11}x_1 + w_{12}x_2 + w_{13}x_3$$
$$y_2 = w_{21}x_1 + w_{22}x_2 + w_{23}x_3$$

**Relación con la IA:**
Esta transformación es el núcleo del Forward Pass en Deep Learning. Cada conexión entre neuronas de diferentes capas tiene un "peso" ($w_{ij}$). La aplicación lineal agrupa todos esos pesos para realizar la traducción masiva de datos. Lo que llamamos "arquitectura" de una red es, en realidad, la definición de las dimensiones de estos espacios y cómo las aplicaciones lineales conectan unos con otros.

### 17.3. Matemática Teórica y Justificación
Sean $V$ y $W$ dos espacios vectoriales sobre $\mathbb{R}$. Una función $T: V \to W$ es una Aplicación Lineal (o transformación lineal) si para todo $u, v \in V$ y cada escalar $\lambda \in \mathbb{R}$ se cumple:

* **Preservación de la suma:** $T(u + v) = T(u) + T(v)$
* **Preservación del producto por escalar:** $T(\lambda v) = \lambda T(v)$

**Justificación:**
¿Por qué exigimos linealidad?
* **Consistencia geométrica:** La linealidad asegura que el origen siempre mapea al origen ($T(\vec{0}) = \vec{0}$). Si esto no ocurriera, la red introduciría sesgos artificiales en cada capa que harían imposible el entrenamiento estable.
* **Estructura de Espacio Vectorial:** El conjunto de todas las aplicaciones lineales de $V$ a $W$, denotado como $\mathcal{L}(V, W)$, es a su vez un espacio vectorial. Esto permite que podamos "sumar" redes neuronales o promediar sus pesos (como se hace en el aprendizaje federado).
* **Composición:** La esencia de la "profundidad" en el Deep Learning es la composición de aplicaciones lineales (seguidas de una no-linealidad). Matemáticamente, componer dos aplicaciones lineales resulta en otra aplicación lineal, lo que permite colapsar operaciones complejas en una sola matriz cuando es necesario.

### 17.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 17.1: El Mapeo entre Espacios</b></summary>
  <br>
  <img src="../img/bloque-4/fig-17-1-mapeo.png" width="100%">
  <p><em>Un diagrama con dos "nubes" ($V$ y $W$). Un vector en $V$ es golpeado por una flecha $T$ y aparece transformado en $W$.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 17.2: Deformación del Espacio (Grid Deformation)</b></summary>
  <br>
  <img src="../img/bloque-4/fig-17-2-deformacion.png" width="100%">
  <p><em>Una rejilla cuadrada perfecta (espacio de entrada) que se ve estirada o rotada tras pasar por la aplicación lineal, mostrando cómo cambian los vectores base.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 17.3: La matriz como Aplicación</b></summary>
  <br>
  <img src="../img/bloque-4/fig-17-3-matriz-aplicacion.png" width="100%">
  <p><em>Un vector entrando en una matriz $A$ y saliendo como un vector de diferente tamaño, ilustrando la dimensión del dominio y el codominio.</em></p>
</details>

---

## Capítulo 18: Núcleo (Kernel) e Imagen: Lo que la IA olvida y lo que recuerda

### 18.1. Explicación para "Dummies": El Gran Filtro
El Núcleo (Kernel) es la información ignorada, mientras que la Imagen (Image) es la detectada y transmitida. Se rigen por el Teorema de la Dimensión.
* **La Imagen (Image):** Es el grupo de personas que logran entrar a la fiesta. Es lo que "sobrevive" al filtro.
* **El Núcleo (Kernel/Null Space):** Es el grupo de personas que se quedan fuera. No importa si son altos, bajos, ricos o pobres; si no cumplen el requisito, para el guardia son "invisibles" o valen cero.

En una red neuronal, el Núcleo es toda la información que la capa decide ignorar (el ruido, el color del fondo, etc.). La Imagen es el conjunto de características que la capa detecta y envía a la siguiente fase. Una IA inteligente es aquella que sabe mandar al Núcleo todo lo que no sirve para la predicción.

### 18.2. Rigor mediante Ejemplo Aplicado: El detector de bordes
Supongamos una capa que procesa nuestra rejilla de $3 \times 3$. Su misión es detectar si hay un cambio de contraste horizontal (un borde).

**El Escenario:**
Si la capa recibe una imagen donde todos los píxeles tienen el mismo brillo (una imagen plana), la salida es un vector cero. Esa imagen plana pertenece al Núcleo de la transformación. La capa ha "borrado" la imagen porque no contiene bordes.
Por el contrario, si recibe una imagen con una línea negra arriba y blanca abajo, la salida será un valor alto. Esa señal forma parte de la Imagen de la transformación.

**Relación con la IA:**
Esto explica por qué la IA puede ser engañada (ataques adversarios). Si añadimos a una imagen de un "gato" un ruido específico que pertenezca al Núcleo de la red, la IA ni siquiera verá ese ruido; para ella, el vector sigue siendo el mismo. Pero si el ruido cae en la Imagen, la IA verá algo que no existe. Entender el Núcleo es entender la ceguera de tu modelo.

### 18.3. Matemática Teórica y Justificación
Sea $T: V \to W$ una aplicación lineal.

**El Núcleo (Kernel):** Es el conjunto de todos los vectores de entrada que mapean al vector nulo de la salida.

$$\text{Ker}(T) = \{ v \in V \mid T(v) = \vec{0}_W \}$$

**La Imagen (Image):** Es el conjunto de todos los vectores en $W$ que son alcanzados por algún vector de $V$.

$$\text{Im}(T) = \{ w \in W \mid \exists v \in V, T(v) = w \}$$

**El Teorema de la Dimensión (Rank-Nullity Theorem):**
Es la ley fundamental de la conservación de la dimensión:

$$\dim(V) = \dim(\text{Ker}(T)) + \dim(\text{Im}(T))$$

**Justificación:**
Este teorema nos dice que no puedes ganar información de la nada. Si tu capa de entrada tiene 1000 neuronas y la de salida 10, has enviado 990 dimensiones al Núcleo. Esas 990 dimensiones de datos han sido destruidas para siempre. En IA, esto se llama cuello de botella (bottleneck). Si el núcleo es demasiado grande, el modelo es demasiado simple (underfitting); si es demasiado pequeño, el modelo no filtra el ruido (overfitting).

### 18.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 18.1: El Sifón Matemático</b></summary>
  <br>
  <img src="../img/bloque-4/fig-18-1-sifon.png" width="100%">
  <p><em>Un espacio $V$ grande donde muchos vectores convergen hacia el punto cero de $W$ (el Núcleo), mientras que otros se proyectan formando una figura en $W$ (la Imagen).</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 18.2: El Espacio de la Ceguera</b></summary>
  <br>
  <img src="../img/bloque-4/fig-18-2-ceguera.png" width="100%">
  <p><em>Una imagen de un dígito con ruido. Una flecha muestra el ruido yendo hacia una caja de "Cero", indicando que pertenece al Núcleo de la capa sensorial.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 18.3: Visualización del Teorema de la Dimensión</b></summary>
  <br>
  <img src="../img/bloque-4/fig-18-3-teorema-dimension.png" width="100%">
  <p><em>Una barra que representa la dimensión total de la entrada, dividida en dos colores: uno para lo que se pierde (Kernel) y otro para lo que se transmite (Imagen/Rango).</em></p>
</details>

---

## Capítulo 19: Representación Matricial: El ADN del procesamiento

### 19.1. Explicación para "Dummies": El manual de instrucciones total
Una Matriz es el manual que codifica una aplicación lineal, permitiendo procesar cualquier dato mediante álgebra computacional.

Si sabes que al píxel 1 lo mueve a la derecha, al píxel 2 lo apaga y al píxel 3 lo vuelve rojo, ya lo sabes todo. Una Matriz es simplemente un manual donde cada columna explica qué le pasa a un vector de la base. Una vez que tienes ese manual, procesar cualquier imagen es solo seguir las instrucciones.

### 19.2. Rigor mediante Ejemplo Aplicado: La Matriz de "Resumen"
Queremos una aplicación lineal $T$ que tome nuestra rejilla de $3 \times 3$ (9 dimensiones) y la reduzca a solo 2 valores: "Brillo promedio arriba" y "Brillo promedio abajo".

**El Escenario:**
Nuestra matriz $A$ tendrá 2 filas (la salida) y 9 columnas (la entrada).
La Fila 1 tendrá valores positivos en las columnas 1, 2 y 3 (píxeles de arriba) y ceros en el resto.
La Fila 2 tendrá valores positivos en las columnas 7, 8 y 9 (píxeles de abajo) y ceros en el resto.
Cuando multiplicas un vector de imagen por esta matriz $A_{2 \times 9}$, el resultado es un vector de 2 dimensiones. Has "comprimido" la realidad.

**Relación con la IA:**
Cada capa de una red neuronal es una matriz. Cuando ves que un modelo tiene "7 mil millones de parámetros", lo que estás viendo es el número total de numeritos dentro de esas matrices. Entrenar la IA es usar el error para cambiar estos números hasta que la matriz aprenda a transformar "píxeles de gato" en el concepto numérico de "gato". La GPU no sabe qué es un gato; solo sabe multiplicar filas por columnas a toda velocidad.

### 19.3. Matemática Teórica y Justificación
Sea $T: V \to W$ una aplicación lineal. Si fijamos una base $B_V$ para $V$ y una base $B_W$ para $W$, existe una única matriz $A$ tal que para todo $v \in V$:

$$[T(v)]_{B_W} = A \cdot [v]_{B_V}$$

La $j$-ésima columna de la matriz $A$ es, por definición, la imagen del vector $e_j$ de la base de entrada, expresada en las coordenadas de la base de salida:

$$A = \begin{bmatrix} [T(e_1)]_{B_W} & [T(e_2)]_{B_W} & \dots & [T(e_n)]_{B_W} \end{bmatrix}$$

**Justificación:**
¿Por qué esta estructura?
* **Isomorfismo:** Existe una correspondencia biunívoca entre el espacio de aplicaciones lineales $\mathcal{L}(V, W)$ y el espacio de matrices $\mathcal{M}_{m \times n}$. Esto nos permite hacer álgebra con matrices en lugar de lidiar con funciones abstractas.
* **Eficiencia Algorítmica:** La multiplicación de matriz por vector es la operación más optimizada de la historia de la computación (gracias a las librerías BLAS y kernels de CUDA).
* **Composición:** La composición de dos capas (aplicaciones lineales) equivale exactamente al producto de sus matrices. Si tienes 100 capas, matemáticamente tienes una sola operación: $A_{100} \dots A_2 A_1$.

### 19.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 19.1: Anatomía de la Matriz</b></summary>
  <br>
  <img src="../img/bloque-4/fig-19-1-anatomia-matriz.png" width="100%">
  <p><em>Un diagrama que muestra cómo cada columna de la matriz "viene" de transformar un vector de la base canónica.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 19.2: El Forward Pass</b></summary>
  <br>
  <img src="../img/bloque-4/fig-19-2-forward-pass.png" width="100%">
  <p><em>Un vector de entrada "chocando" con una rejilla de números (matriz) y convirtiéndose en un vector de salida.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 19.3: Composición y Producto</b></summary>
  <br>
  <img src="../img/bloque-4/fig-19-3-composicion-producto.png" width="100%">
  <p><em>Dos cajas (matrices) conectadas en serie, mostrando que el efecto total es el producto de ambas matrices.</em></p>
</details>

---

## Capítulo 20: El Cambio de Base: Cambiando de perspectiva

### 20.1. Explicación para "Dummies": Las gafas del experto
La Matriz de Cambio de Base permite ver los datos desde la perspectiva más simplificada posible.

La realidad (el baile) no ha cambiado. Lo que ha cambiado es tu base (tu punto de vista).
En la IA, una imagen en "base píxel" es solo un montón de puntos. Pero si cambiamos la base a una de "frecuencias" o "bordes", lo que era ruido se convierte en estructuras claras. El cambio de base es como ponerle a la IA las gafas que resaltan lo importante y oscurecen lo irrelevante.

### 20.2. Rigor mediante Ejemplo Aplicado: De Píxeles a "Conceptos"
Volvemos a nuestra rejilla de $3 \times 3$. Hasta ahora, nuestra base eran los píxeles individuales ($e_i$).

**El Escenario:**
Supongamos que en lugar de usar píxeles, queremos usar una base $B'$ que represente "patrones globales".
* Vector de base 1 ($v'_1$): Todos los píxeles encendidos (Brillo general).
* Vector de base 2 ($v'_2$): Solo píxeles de la izquierda encendidos vs derecha apagados (Contraste lateral).

Si una imagen tiene un valor de $0.9$ en la coordenada del vector $v'_1$, sabemos instantáneamente que es una imagen clara, sin tener que mirar los 9 píxeles uno a uno.

**Relación con la IA:**
Esto es lo que hace el Análisis de Componentes Principales (PCA) o las Transformadas de Fourier. En lugar de procesar los datos en el espacio "crudo", la IA los proyecta en una base donde la información está más concentrada. Si eliges la base adecuada, un problema que requería 1000 neuronas puede resolverse con solo 10. El "ahorro" computacional de los modelos modernos depende totalmente de encontrar estas bases óptimas.

### 20.3. Matemática Teórica y Justificación
Sea $V$ un espacio vectorial con dos bases distintas: la base antigua $B$ y la base nueva $B'$. Todo vector $v \in V$ tiene dos representaciones distintas: $[v]_B$ y $[v]_{B'}$.

Existe una matriz única e invertible $P$, llamada Matriz de Cambio de Base (o de transición), tal que:

$$[v]_B = P [v]_{B'}$$

Las columnas de $P$ son simplemente los vectores de la base nueva expresados en función de la base antigua.

**Justificación:**
* **Invertibilidad:** Por definición, una base debe ser linealmente independiente, lo que garantiza que $P$ siempre tenga inversa ($\det(P) \neq 0$). Esto asegura que no perdemos información al cambiar de perspectiva; siempre podemos volver al origen usando $P^{-1}$.
* **Transformación de Aplicaciones:** Si una capa de la IA (matriz $A$) se expresa en una base distinta, su nueva forma será $A' = P^{-1} A P$. Esta operación (semejanza de matrices) es la clave para la Diagonalización, que veremos más adelante, y que permite que la IA calcule potencias de matrices (capas recurrentes) en tiempo récord.

### 20.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 20.1: Dos Rejillas, Un Vector</b></summary>
  <br>
  <img src="../img/bloque-4/fig-20-1-rejillas.png" width="100%">
  <p><em>Muestra un mismo vector sobrepuesto en dos sistemas de coordenadas: uno recto (estándar) y uno rotado y estirado (nueva base).</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 20.2: La Matriz como Puente</b></summary>
  <br>
  <img src="../img/bloque-4/fig-20-2-puente.png" width="100%">
  <p><em>Un diagrama de flujo donde un vector viaja de la Base A a la Base B a través de la matriz $P$, y regresa a través de $P^{-1}$.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 20.3: Compresión de Información (PCA)</b></summary>
  <br>
  <img src="../img/bloque-4/fig-20-3-pca.png" width="100%">
  <p><em>Una nube de puntos estirada en diagonal. Se muestran los ejes de la base antigua ($X, Y$) y los nuevos ejes alineados con la forma de la nube, demostrando que un solo eje nuevo explica casi todos los datos.</em></p>
</details>

---

## Capítulo 21: El Determinante: El factor de escala del universo

### 21.1. Explicación para "Dummies": El medidor de "Zoom"
El Determinante mide cómo una transformación altera el volumen de la información.
* Si el rombo ahora ocupa el doble, el Determinante de esa matriz es $2$. La capa ha expandido el espacio.
* Si el rombo se ha encogido a la mitad, el determinante es $0.5$.
* Si el cuadrado se ha aplastado tanto que ahora es solo una línea, su área es $0$. El determinante es $0$.

En la IA, el determinante nos dice si la transformación conserva el "volumen" de la información o si la está comprimiendo hasta hacerla desaparecer.

### 21.2. Rigor mediante Ejemplo Aplicado: Estabilidad y Colapso
Supongamos que estamos entrenando una red y una de las matrices de pesos $W$ termina teniendo un determinante de $0$.

**El Escenario:**
Si $\det(W) = 0$, significa que la matriz ha "aplastado" al menos una dimensión de los datos. Si tenías información en 3D (ej. color, textura y forma) y el determinante es $0$, la IA ha decidido que una de esas cosas no existe, fusionándola con las demás.

**Relación con la IA:**
Esto es crítico en los Modelos Generativos de Flujo (Normalizing Flows). Estos modelos necesitan transformar una distribución de probabilidad simple en una compleja sin perder información. Para ello, deben asegurar que el determinante de sus transformaciones (el Jacobiano) nunca sea cero. Si el determinante colapsa, la IA sufre de "colapso de modo", donde empieza a generar siempre la misma imagen porque ha perdido las dimensiones que daban variedad al mundo.

### 21.3. Matemática Teórica y Justificación
El Determinante es una función $\det: \mathcal{M}_{n \times n} \to \mathbb{R}$ que asigna un escalar a cada matriz cuadrada. Posee tres propiedades definitorias que dictan su comportamiento:
* **Multilinealidad:** Es lineal respecto a cada fila (o columna) de forma independiente.
* **Alternancia:** Si intercambias dos filas, el signo del determinante cambia (refleja la orientación del espacio).
* **Normalidad:** El determinante de la matriz identidad es $1$ ($\det(I) = 1$).

**Justificación:**
¿Por qué el determinante decide la Invertibilidad?
Si $\det(A) \neq 0$, la transformación es una biyección: puedes ir de la entrada a la salida y volver atrás sin pérdida. Si $\det(A) = 0$, la matriz es singular. Matemáticamente, esto significa que el núcleo (Kernel) de la aplicación no es solo el vector cero; hay toda una dirección de datos que ha sido borrada. En términos de optimización, una matriz con determinante cercano a cero hace que el cálculo del gradiente explote o desaparezca, rompiendo el entrenamiento.

### 21.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 21.1: El Factor de Área</b></summary>
  <br>
  <img src="../img/bloque-4/fig-21-1-area.png" width="100%">
  <p><em>Un cuadrado unitario transformándose en un paralelogramo. Se sombrean ambas áreas y se muestra la relación numérica igual al determinante.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 21.2: El Cambio de Orientación</b></summary>
  <br>
  <img src="../img/bloque-4/fig-21-2-orientacion.png" width="100%">
  <p><em>Una mano derecha transformándose en una mano izquierda (espejo), ilustrando un determinante negativo (el volumen se mantiene, pero la orientación se invierte).</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 21.3: El Colapso de Dimensión</b></summary>
  <br>
  <img src="../img/bloque-4/fig-21-3-colapso-dimension.png" width="100%">
  <p><em>Un cubo 3D siendo proyectado por una matriz de determinante cero, convirtiéndose en una "hoja" 2D sin volumen.</em></p>
</details>

---

## Capítulo 22: Valores y Vectores Propios: El esqueleto del movimiento

### 22.1. Explicación para "Dummies": Las líneas que no se tuercen
Los Vectores Propios (Eigenvectors) son direcciones que no rotan bajo una transformación, escaladas por sus Valores Propios (Eigenvalues).
* **Vectores Propios (Eigenvectors):** Son esas direcciones privilegiadas que se mantienen fieles a su orientación original a pesar de la transformación.
* **Valores Propios (Eigenvalues):** Es el factor de escala. Nos dice cuánto se estira (si es $>1$) o cuánto se encoge (si es $0 < \lambda < 1$) el vector en esa dirección.

En la IA, estas son las "arterias principales" por donde fluye la información. Todo lo demás es ruido que acaba rotando y desapareciendo.

### 22.2. Rigor mediante Ejemplo Aplicado: PCA y la esencia de los datos
Imagina que tienes una nube de datos sobre el crecimiento de árboles (altura y diámetro). Están muy relacionados: a más altura, más diámetro.

**El Escenario:**
Si calculamos la matriz de covarianza de esos datos y extraemos sus vectores propios, ocurrirá algo asombroso:
* El Vector Propio principal apuntará exactamente en la dirección de la línea que mejor resume la relación entre altura y diámetro.
* El Valor Propio asociado nos dirá cuánta información (varianza) hay en esa dirección.

**Relación con la IA:**
Esto es el Análisis de Componentes Principales (PCA). La IA utiliza los vectores propios para "simplificar" el universo. Si un valor propio es casi cero, la IA sabe que esa dirección no tiene información útil y puede borrarla sin miedo. Es el método matemático para pasar de un problema de 1.000 variables a uno de 5, quedándonos solo con las "líneas maestras" de la realidad.

### 22.3. Matemática Teórica y Justificación
Sea $A$ una matriz cuadrada. Un vector no nulo $v$ es un vector propio de $A$ si existe un escalar $\lambda$ (llamado valor propio) tal que:

$$A v = \lambda v$$

Esta ecuación es profunda porque transforma una operación matricial compleja ($A \times v$) en una simple multiplicación escalar ($\lambda \times v$).

**Cómo encontrarlos:**
Para que la ecuación $(A - \lambda I)v = \vec{0}$ tenga soluciones distintas de cero, la matriz $(A - \lambda I)$ debe ser singular (colapsar el espacio). Por tanto, resolvemos el Polinomio Característico:

$$\det(A - \lambda I) = 0$$

**Justificación:**
¿Por qué es vital en el aprendizaje profundo?
* **Estabilidad del Gradiente:** En las redes neuronales recurrentes (RNN), si los valores propios de las matrices de pesos son mayores que 1, el gradiente "explota" al multiplicarse muchas veces. Si son menores que 1, el gradiente "se desvanece".
* **Convergencia:** La velocidad a la que una IA aprende depende de la relación entre el valor propio más grande y el más pequeño de la matriz de curvatura (Hessiana). Si están muy descompensados, la IA "zigzaguea" y tarda siglos en optimizar.

### 22.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 22.1: El Estiramiento Puro</b></summary>
  <br>
  <img src="../img/bloque-4/fig-22-1-estiramiento.png" width="100%">
  <p><em>Una rejilla deformada donde se resaltan dos flechas (vectores propios) que no han rotado, solo han cambiado su longitud.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 22.2: Estabilidad vs. Explosión</b></summary>
  <br>
  <img src="../img/bloque-4/fig-22-2-estabilidad.png" width="100%">
  <p><em>Una secuencia de vectores siendo multiplicados repetidamente por una matriz. Si $\lambda > 1$, la flecha se sale del gráfico; si $\lambda < 1$, colapsa hacia el origen.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 22.3: El Elipsoide de los Datos</b></summary>
  <br>
  <img src="../img/bloque-4/fig-22-3-elipsoide.png" width="100%">
  <p><em>Una nube de puntos en 3D envuelta en un elipsoide cuyos ejes principales son los vectores propios, con longitudes proporcionales a los valores propios.</em></p>
</details>

---

## Capítulo 23: Diagonalización de Matrices: El truco de la eficiencia infinita

### 23.1. Explicación Directa: El interruptor de la simplicidad
La Diagonalización permite desacoplar dimensiones para operar de forma independiente y eficiente.
En matemáticas, una matriz diagonal es aquella que solo tiene números en la diagonal principal y ceros en todo lo demás. Operar con ella es un regalo: si quieres elevarla al cuadrado, solo elevas los números de la diagonal. Si quieres aplicarla a un millón de vectores, es una simple multiplicación escalar. Diagonalizar una matriz compleja es encontrar el "punto de vista" (la base) donde esa matriz se vuelve diagonal.

### 23.2. Rigor Aplicado: El problema de las potencias
En IA, especialmente en Redes Neuronales Recurrentes (RNN) o en algoritmos de recomendación basados en Grafos, necesitamos aplicar la misma matriz de pesos cientos de veces ($A^{100}$).

**El Escenario:**
Si intentas multiplicar una matriz densa de $10.000 \times 10.000$ por sí misma 100 veces, tu servidor colapsará por la carga computacional y el error acumulado.
Sin embargo, si diagonalizas $A$ como $A = P D P^{-1}$:

$$A^n = (P D P^{-1})^n = P D^n P^{-1}$$

**La ventaja:**
Solo tienes que elevar a la potencia $n$ los elementos de la diagonal de $D$. Lo que antes requería trillones de operaciones ahora se resuelve en microsegundos. Si tu modelo de IA es rápido, es porque alguien, en algún lugar del código, está aprovechando una descomposición similar a esta.

### 23.3. Matemática Teórica y Justificación
Una matriz cuadrada $A$ es diagonalizable si y solo si tiene $n$ vectores propios linealmente independientes.

Si esto se cumple, existe una matriz invertible $P$ (cuyas columnas son los vectores propios) y una matriz diagonal $D$ (cuyos elementos son los valores propios) tales que:

$$A = P D P^{-1}$$

**Justificación Técnica:**
* **Independencia de Ejes:** La diagonalización nos dice que la transformación lineal que representa $A$ no es más que un escalado puro si cambiamos a la base de sus vectores propios.
* **Semejanza:** Decimos que $A$ y $D$ son matrices semejantes. Representan la misma aplicación lineal pero en bases distintas.
* **Criterio de Diagonalización:** No todas las matrices se pueden diagonalizar. Si una matriz no tiene suficientes vectores propios (debido a multiplicidades algebraicas mayores que las geométricas), se dice que es una matriz defectiva. En ingeniería, esto es una señal de que tu sistema tiene redundancias mal gestionadas.

### 23.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 23.1: El Recableado de la Matriz</b></summary>
  <br>
  <img src="../img/bloque-4/fig-23-1-recableado.png" width="100%">
  <p><em>Una matriz llena de números transformándose en una matriz con solo la diagonal iluminada, mediante el paso por las matrices $P$ y $P^{-1}$.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 23.2: El Atajo del Cálculo</b></summary>
  <br>
  <img src="../img/bloque-4/fig-23-2-atajo-calculo.png" width="100%">
  <p><em>Un diagrama que compara el camino largo (multiplicar $A$ muchas veces) frente al atajo de diagonalizar y elevar solo la diagonal, mostrando la diferencia en pasos computacionales.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 23.3: Desacoplamiento de Dimensiones</b></summary>
  <br>
  <img src="../img/bloque-4/fig-23-3-desacoplamiento.png" width="100%">
  <p><em>Un sistema de ejes donde un vector se mueve de forma errática (base estándar) vs. un sistema donde se mueve solo a lo largo de los ejes (base de vectores propios).</em></p>
</details>

---

## Capítulo 24: Descomposición en Valores Singulares (SVD): El ADN de la compresión

### 24.1. Explicación Directa: La autopsia de los datos
La Descomposición en Valores Singulares (SVD) permite identificar los valores singulares que dominan la estructura de cualquier matriz de datos.
* Giro ($V^T$): Orientas la arcilla para verla desde el mejor ángulo posible.
* Estiramiento ($\Sigma$): Estiras la arcilla en las direcciones que tienen más volumen (información) y aplastas las que no sirven.
* Giro final ($U$): Colocas el resultado en el espacio de destino.

A diferencia de la diagonalización, que requiere matrices cuadradas y "especiales", la SVD funciona con cualquier tabla de datos. Es universal.

### 24.2. Rigor Aplicado: El sistema de recomendación
Imagina una matriz donde las filas son Usuarios y las columnas son Películas. Los números son las puntuaciones. Es una matriz gigantesca y llena de huecos (porque nadie ve todas las películas).

**El Escenario:**
Al aplicar SVD, la IA descompone esta matriz en tres:
* $U$ (Matriz izquierda): ¿A qué "perfil" pertenece cada usuario? (ej. ¿Le gusta el drama?).
* $\Sigma$ (Matriz central): ¿Qué géneros son los más importantes en la base de datos?
* $V^T$ (Matriz derecha): ¿Qué películas definen cada género?

**La ventaja:**
La IA no necesita saber que "Matrix" es Ciencia Ficción. La SVD descubre por sí sola que hay un patrón (un "valor singular" fuerte) que conecta a ciertos usuarios con ciertas películas. Al ignorar los valores singulares pequeños, la IA elimina el "ruido" (puntuaciones aleatorias) y se queda con la esencia del gusto del usuario. Esto es el Espacio Latente.

### 24.3. Matemática Teórica y Justificación
Cualquier matriz $A_{m \times n}$ puede descomponerse de la forma:

$$A = U \Sigma V^T$$

Donde:
* $U_{m \times m}$: Matriz ortogonal cuyas columnas son los vectores propios de $AA^T$ (vectores singulares a izquierda). Representan el espacio de salida.
* $\Sigma_{m \times n}$: Matriz diagonal (no necesariamente cuadrada) que contiene las raíces cuadradas de los valores propios de $A^T A$, ordenados de mayor a menor ($\sigma_1 \ge \sigma_2 \ge \dots \ge 0$).
* $V^T_{n \times n}$: Matriz ortogonal cuyas filas son los vectores propios de $A^T A$ (vectores singulares a derecha). Representan el espacio de entrada.

**Justificación Técnica:**
* **Aproximación de Bajo Rango:** Si te quedas solo con los $k$ valores singulares más grandes, obtienes la mejor aproximación posible de la matriz original en términos de energía (Teorema de Eckart-Young). Esto es la base de la compresión de imágenes y de los modelos de lenguaje reducidos.
* **Estabilidad Numérica:** A diferencia de la inversión de matrices clásica, la SVD es extremadamente robusta. Si una matriz es casi singular, la SVD te lo dice exactamente a través de sus valores singulares, evitando errores de división por cero en el código de entrenamiento.

### 24.4. Herramientas Visuales Sugeridas

<details>
  <summary><b>🖼️ Figura 24.1: El Estiramiento del Hiperelipsoide</b></summary>
  <br>
  <img src="../img/bloque-4/fig-24-1-estiramiento-svd.png" width="100%">
  <p><em>Una esfera siendo transformada en un elipsoide. Los ejes del elipsoide son las columnas de $U$ y sus longitudes son los valores singulares $\sigma_i$.</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 24.2: Compresión de Imagen por SVD</b></summary>
  <br>
  <img src="../img/bloque-4/fig-24-2-compresion-svd.png" width="100%">
  <p><em>Una imagen de un rostro que se va volviendo más nítida a medida que sumamos más componentes de la SVD ($k=5, 20, 50$).</em></p>
</details>

<details>
  <summary><b>🖼️ Figura 24.3: La Matriz como Suma de Rango 1</b></summary>
  <br>
  <img src="../img/bloque-4/fig-24-3-suma-rango-1.png" width="100%">
  <p><em>Una visualización de cómo $A$ es en realidad la suma de varias "capas" de información, donde las primeras capas contienen la estructura principal y las últimas el detalle/ruido (suma ponderada de los productos externos de $u_i$ y $v_i^T$).</em></p>
</details>
