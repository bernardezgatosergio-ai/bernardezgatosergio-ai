# 📙 Cuadernillo III — Álgebra sobre Iris (Temas 1–15)

Aplicación Práctica · Fundamentos, Geometría Euclídea y Matrices — todos calculados con los datos reales de Fisher (1936).

**Vectores media de cada especie ($\mu \in \mathbb{R}^4$) y media global:**
* **Iris setosa:** $\mu_s = [5.006, 3.428, 1.462, 0.246]^T$
* **Iris versicolor:** $\mu_{ve} = [5.936, 2.770, 4.260, 1.326]^T$
* **Iris virginica:** $\mu_{vi} = [6.588, 2.974, 5.552, 2.026]^T$
* **Media global:** $\mu_g = [5.843, 3.057, 3.758, 1.199]^T$

---

## 📦 BLOQUE I: FUNDAMENTOS

### Tema 01 | Espacio Vectorial (¿Dónde viven nuestras flores?)

**🌸 Dummies — La intuición**
Cada flor Iris es un punto en el espacio. No el espacio 3D de la vida cotidiana, sino uno de **cuatro dimensiones**: longitud del sépalo, ancho del sépalo, longitud del pétalo y ancho del pétalo. Un *espacio vectorial* es un "contenedor" donde puedes sumar objetos y multiplicarlos por números, y el resultado sigue viviendo dentro. Las flores Iris son puntos en ese contenedor: $\mathbb{R}^4$. Si sumas dos flores coordenada a coordenada, obtienes otra "flor virtual" en $\mathbb{R}^4$. Si multiplicas todas las medidas por 2, sigues en $\mathbb{R}^4$. Esa es la esencia.

**∑ Algebraico — La definición**
Un **espacio vectorial** sobre $\mathbb{R}$ es un conjunto $V$ con dos operaciones que satisfacen 8 axiomas:
Adición: $+: V \times V \to V$
Escalar: $\cdot: \mathbb{R} \times V \to V$
* (A1) $u + v = v + u$ (conmutatividad)
* (A2) $(u+v)+w = u+(v+w)$ (asociatividad)
* (A3) $\exists 0 \in V : v + 0 = v$ (elemento neutro)
* (A4) $\forall v \exists(-v) : v + (-v) = 0$ (inverso aditivo)
* (S1) $\alpha(\beta v) = (\alpha\beta)v$ (comp. escalar)
* (S2) $1 \cdot v = v$ (escalar unidad)
* (S3) $\alpha(u+v) = \alpha u + \alpha v$ (distributiva I)
* (S4) $(\alpha+\beta)v = \alpha v + \beta v$ (distributiva II)

**🔢 Cálculo con el Iris — datos reales Fisher 1936**
Verificación A1: $\mu_s + \mu_{ve} = \mu_{ve} + \mu_s$
$$\mu_s + \mu_{ve} = [10.942, 6.198, 5.722, 1.572]^T$$
Verificación S2: $1 \cdot \mu_s = \mu_s$
$$1 \cdot [5.006, 3.428, 1.462, 0.246]^T = [5.006, 3.428, 1.462, 0.246]^T$$
Flor media global como combinación lineal válida:
$$\mu_{global} = \frac{1}{3}\mu_s + \frac{1}{3}\mu_{ve} + \frac{1}{3}\mu_{vi} = [5.843, 3.057, 3.758, 1.199]^T \in \mathbb{R}^4$$
> **🔑 Clave:** Cada flor Iris es un vector en $\mathbb{R}^4$ que satisface los 8 axiomas. La "flor media global" es una combinación lineal válida: sigue siendo un punto del mismo espacio.

---

### Tema 02 | Subespacio Vectorial (Subestructuras dentro de $\mathbb{R}^4$)

**🌸 Dummies**
Un *subespacio* es un "cuarto" dentro del "edificio" $\mathbb{R}^4$. Un subconjunto de flores tal que si las sumas o escales, el resultado sigue dentro del mismo cuarto. Por ejemplo: el conjunto de vectores con ceros en las dos primeras coordenadas, $(0,0,x_3,x_4)$, forma un plano dentro de $\mathbb{R}^4$ — un subespacio de dimensión 2 que sólo contiene "flores sin sépalo". Los subespacios siempre pasan por el origen: son "planos que contienen el cero".

**∑ Algebraico**
$W \subseteq V$ es subespacio si y sólo si cumple tres condiciones (necesarias y suficientes):
* (W1) $0 \in W$ (contiene el origen)
* (W2) $u, v \in W \implies u + v \in W$ (cerrado en adición)
* (W3) $v \in W, \alpha \in \mathbb{R} \implies \alpha v \in W$ (cerrado en escalar)
Equivalente compacto: $W$ es subespacio $\iff \forall \alpha, \beta \in \mathbb{R}, \forall u, v \in W : \alpha u + \beta v \in W$

**🔢 Cálculo con el Iris**
$W_1$ — subespacio de variables de pétalo: $W_1 = \{ (0, 0, x_3, x_4) \in \mathbb{R}^4 : x_3, x_4 \in \mathbb{R} \}$
* (W1) $(0,0,0,0) \in W_1$ (✓)
* (W2) $(0,0,1.462,0.246) + (0,0,4.260,1.326) = (0,0,5.722,1.572) \in W_1$ (✓)
* (W3) $3 \cdot (0,0,1.462,0.246) = (0,0,4.386,0.738) \in W_1$ (✓)
$W_1$ es subespacio de dimensión 2.

¿Es el conjunto $\{\mu_s, \mu_{ve}, \mu_{vi}\}$ un subespacio?
* (W1): $(0,0,0,0) \notin \{\mu_s, \mu_{ve}, \mu_{vi}\}$ (✗ NO es subespacio). Pero $\text{span}\{\mu_s, \mu_{ve}, \mu_{vi}\}$ (la envolvente lineal) SÍ lo es.
> **🔑 Clave:** Los tres vectores media NO forman un subespacio por sí solos (fallan W1), pero su envolvente lineal sí lo es.

---

### Tema 03 | Independencia Lineal (¿Podemos recuperar una especie a partir de las otras?)

**🌸 Dummies**
Si los tres vectores-media fueran *linealmente dependientes*, significaría que uno es simplemente mezcla de los otros dos: la Setosa sería una combinación de Versicolor y Virginica. Si no puede expresarse así, son *linealmente independientes*: cada especie aporta información morfológica nueva e irreducible. Visualmente: si tres vectores "apuntan en direcciones genuinamente distintas", son independientes. Si uno de ellos vive en el plano definido por los otros dos, son dependientes.

**∑ Algebraico**
Los vectores $v_1, \dots, v_k \in V$ son **linealmente independientes** si y sólo si:
$$\alpha_1 v_1 + \alpha_2 v_2 + \dots + \alpha_k v_k = \mathbf{0} \implies \alpha_1 = \alpha_2 = \dots = \alpha_k = 0$$
Equivalente: ninguno es combinación lineal de los demás. Criterio matricial: si $M = [v_1|v_2|\dots|v_k]$, entonces son LI $\iff \text{rang}(M) = k \iff \ker(M) = \{\mathbf{0}\}$.

**🔢 Cálculo con el Iris**
Matriz $M = [\mu_s | \mu_{ve} | \mu_{vi}]$ — sistema $\alpha_1\mu_s + \alpha_2\mu_{ve} + \alpha_3\mu_{vi} = 0$:
$$M = \begin{bmatrix} 5.006 & 5.936 & 6.588 \\ 3.428 & 2.770 & 2.974 \\ 1.462 & 4.260 & 5.552 \\ 0.246 & 1.326 & 2.026 \end{bmatrix}$$
Eliminación de Gauss (pivote = 5.006):
$F_2 \leftarrow F_2 - (3.428/5.006) \cdot F_1 = F_2 - 0.685 \cdot F_1$
$F_3 \leftarrow F_3 - (1.462/5.006) \cdot F_1 = F_3 - 0.292 \cdot F_1$
$F_4 \leftarrow F_4 - (0.246/5.006) \cdot F_1 = F_4 - 0.049 \cdot F_1$
Tras escalonar, todos los pivotes son $\neq 0$. Por tanto, $\text{rang}(M) = 3$.
> **🔑 Clave:** Nº columnas = 3 = rango $\implies$ columnas LI. Las 3 especies son morfológicamente distinguibles: ninguna puede "sintetizarse" como mezcla lineal de las otras dos.

---

### Tema 04 | Base y Dimensión (El vocabulario mínimo del espacio Iris)

**🌸 Dummies**
Una *base* es el vocabulario mínimo con el que puedes describir cualquier flor. Si tienes 4 vectores linealmente independientes que generan todo $\mathbb{R}^4$, son una base. La *dimensión* es el tamaño de ese vocabulario mínimo. $\mathbb{R}^4$ tiene dimensión 4: necesitas exactamente 4 medidas independientes para describir completamente una flor Iris. Hay infinitas bases posibles para $\mathbb{R}^4$, pero todas tienen exactamente 4 elementos.

**∑ Algebraico**
$\mathcal{B} = \{b_1, \dots, b_n\}$ es base de $V$ si cumple dos condiciones simultáneas:
* (B1) $\mathcal{B}$ es linealmente independiente.
* (B2) $\text{span}(\mathcal{B}) = V$ ($\mathcal{B}$ genera todo $V$).
$\dim(V) =$ cardinalidad de cualquier base de $V$. Teorema del completamiento: Todo LI se extiende a una base; todo generador contiene una base.

**🔢 Cálculo con el Iris**
Base canónica de $\mathbb{R}^4$ (las 4 "medidas puras"):
$e_1 = [1, 0, 0, 0]^T$ (longitud sépalo)
$e_2 = [0, 1, 0, 0]^T$ (ancho sépalo)
$e_3 = [0, 0, 1, 0]^T$ (longitud pétalo)
$e_4 = [0, 0, 0, 1]^T$ (ancho pétalo)
Cualquier flor en esta base: $\mu_s = 5.006 e_1 + 3.428 e_2 + 1.462 e_3 + 0.246 e_4$.

Base alternativa orientada a diferencias entre especies:
$b_1 = \mu_s = [5.006, 3.428, 1.462, 0.246]^T$
$b_2 = \mu_{ve} - \mu_s = [0.930, -0.658, 2.798, 1.080]^T$
$b_3 = \mu_{vi} - \mu_{ve} = [0.652, 0.204, 1.292, 0.700]^T$
$b_4 = e_2 = [0, 1, 0, 0]^T$
El $\text{rang}([b_1|b_2|b_3|b_4]) = 4 \implies$ sí es base. $\dim(\mathbb{R}^4) = 4$.

---

### Tema 05 | Combinación Lineal y Span (El espacio generado por las especies)

**🌸 Dummies**
Una *combinación lineal* es una mezcla ponderada de vectores: multiplicas cada uno por un escalar y sumas. Una "flor sintética" entre Setosa y Versicolor sería $0.5\mu_s + 0.5\mu_{ve}$. El *span* de un conjunto es la totalidad de combinaciones lineales posibles: todas las flores que se pueden generar mezclando esas semillas con cualquier proporción.

**∑ Algebraico**
Combinación lineal de $S = \{v_1, \dots, v_k\}$: $w = \alpha_1 v_1 + \dots + \alpha_k v_k$, con $\alpha_i \in \mathbb{R}$.
$\text{span}(S) = \{ \alpha_1 v_1 + \dots + \alpha_k v_k : \alpha_1, \dots, \alpha_k \in \mathbb{R} \}$
El span es el MENOR subespacio que contiene a $S$.

**🔢 Cálculo con el Iris**
Interpolación convexa (flor intermedia):
$f_1 = 0.5 \mu_s + 0.5 \mu_{ve} = 0.5[5.006, 3.428, 1.462, 0.246] + 0.5[5.936, 2.770, 4.260, 1.326]$
$f_1 = [5.471, 3.099, 2.861, 0.786]^T$

Extrapolación (flor más allá de Virginica):
$f_2 = 2 \mu_{vi} - \mu_{ve} = 2[6.588, 2.974, 5.552, 2.026] - [5.936, 2.770, 4.260, 1.326]$
$f_2 = [7.240, 3.178, 6.844, 2.726]^T$

¿Qué genera $\text{span}\{\mu_s, \mu_{ve}, \mu_{vi}\}$? Son 3 vectores LI, por lo que generan un subespacio de dimensión 3.
$\text{span}\{\mu_s, \mu_{ve}, \mu_{vi}\} \cong \mathbb{R}^3 \subsetneq \mathbb{R}^4$.
> **🔑 Clave:** Es un hiperplano 3D dentro de $\mathbb{R}^4$. No es todo $\mathbb{R}^4$: hay "flores inaccesibles" desde las 3 medias.

---

## 📦 BLOQUE II: GEOMETRÍA

### Tema 06 | Producto Escalar (La geometría empieza aquí)

**🌸 Dummies**
El *producto escalar* le da a nuestro espacio $\mathbb{R}^4$ una noción de ángulo y longitud. Sin él, $\mathbb{R}^4$ sólo tiene estructura algebraica. Con él, tiene geometría. Intuitivamente: el producto escalar de dos flores mide "cuánto comparten la misma dirección". Si tienen proporciones similares, su producto escalar es grande. Si sus variaciones son ortogonales, es cero.

**∑ Algebraico**
Axiomas del producto interno $\langle \cdot, \cdot \rangle : V \times V \to \mathbb{R}$:
* (P1) $\langle u, v \rangle = \langle v, u \rangle$ (simetría)
* (P2) $\langle \alpha u + \beta v, w \rangle = \alpha\langle u, w \rangle + \beta\langle v, w \rangle$ (linealidad 1er arg)
* (P3) $\langle v, v \rangle \geq 0$, $\langle v, v \rangle = 0 \iff v = 0$ (def. positiva)
Producto escalar estándar en $\mathbb{R}^n$: $\langle u, v \rangle = u^T v = \sum u_i v_i$.
Desigualdad de Cauchy-Schwarz: $|\langle u, v \rangle|^2 \leq \langle u, u \rangle \cdot \langle v, v \rangle$.

**🔢 Cálculo con el Iris**
$$\langle \mu_s, \mu_{ve} \rangle = 5.006(5.936) + 3.428(2.770) + 1.462(4.260) + 0.246(1.326) = 45.766$$
$$\langle \mu_s, \mu_{vi} \rangle = 5.006(6.588) + 3.428(2.974) + 1.462(5.552) + 0.246(2.026) = 51.788$$
$$\langle \mu_{ve}, \mu_{vi} \rangle = 5.936(6.588) + 2.770(2.974) + 4.260(5.552) + 1.326(2.026) = 73.680$$
Versicolor y Virginica tienen mayor producto escalar: apuntan más en la misma dirección.
Verificación Cauchy-Schwarz $|\langle \mu_s, \mu_{ve} \rangle|^2 \leq \langle \mu_s, \mu_s \rangle \cdot \langle \mu_{ve}, \mu_{ve} \rangle$:
$45.766^2 = 2094.5 \leq 39.010 \times 62.815 = 2450.5$ (✓).

---

### Tema 07 | Norma y Distancia Euclídea (¿Cuánto se parecen dos flores?)

**🌸 Dummies**
La *norma* es la longitud de un vector-flor en $\mathbb{R}^4$. La *distancia euclídea* entre dos flores es la longitud del vector diferencia: cuánto difieren en todas sus medidas simultáneamente. Es el teorema de Pitágoras generalizado a 4 dimensiones: $d^2 = \Delta x_1^2 + \Delta x_2^2 + \Delta x_3^2 + \Delta x_4^2$.

**∑ Algebraico**
$\|v\| = \sqrt{\langle v, v \rangle} = \sqrt{\sum v_i^2}$.
Propiedades: $\|v\| \geq 0$; $\|\alpha v\| = |\alpha|\|v\|$; $\|u+v\| \leq \|u\| + \|v\|$ (desigualdad triangular).
$d(u,v) = \|u-v\| = \sqrt{\sum(u_i - v_i)^2}$.

**🔢 Cálculo con el Iris**
Normas:
$\|\mu_s\| = \sqrt{25.060+11.751+2.138+0.061} = \sqrt{39.010} = 6.246$
$\|\mu_{ve}\| = \sqrt{35.236+7.673+18.148+1.758} = \sqrt{62.815} = 7.926$
$\|\mu_{vi}\| = \sqrt{43.401+8.845+30.825+4.105} = \sqrt{87.176} = 9.337$

Distancias euclídeas:
$d(\mu_s, \mu_{ve}) = \|[0.930, -0.658, 2.798, 1.080]\| = \sqrt{10.293} = 3.208$
$d(\mu_s, \mu_{vi}) = \|[1.582, -0.454, 4.090, 1.780]\| = \sqrt{22.604} = 4.754$
$d(\mu_{ve}, \mu_{vi}) = \|[0.652, 0.204, 1.292, 0.700]\| = \sqrt{2.626} = 1.621$
> **🔑 Clave:** Setosa está muy lejos de las otras dos ($d>3.2$). Versicolor y Virginica son próximas ($d=1.621$).

---

### Tema 08 | Ángulo entre Vectores (La similitud de dirección)

**🌸 Dummies**
El ángulo entre dos vectores mide cuánto "apuntan en la misma dirección". Ángulo=0° significa misma dirección (sólo escala diferente). Ángulo=90° significa ortogonales. El coseno del ángulo (*similitud coseno*) es usado en ML para medir similitud ignorando la escala.

**∑ Algebraico**
$\cos \theta = \frac{\langle u, v \rangle}{\|u\|\|v\|} \implies \theta = \arccos\left(\frac{\langle u, v \rangle}{\|u\|\|v\|}\right) \in [0^\circ, 180^\circ]$
$\text{sim}(u,v) = \cos \theta \in [-1, 1]$.

**🔢 Cálculo con el Iris**
$\cos \theta(\mu_s, \mu_{ve}) = \frac{45.766}{6.246 \times 7.926} = \frac{45.766}{49.495} = 0.9247 \implies \theta = 22.4^\circ$
$\cos \theta(\mu_s, \mu_{vi}) = \frac{51.788}{6.246 \times 9.337} = \frac{51.788}{58.319} = 0.8880 \implies \theta = 27.2^\circ$
$\cos \theta(\mu_{ve}, \mu_{vi}) = \frac{73.680}{7.926 \times 9.337} = \frac{73.680}{74.005} = 0.9956 \implies \theta = 5.4^\circ$
> **🔑 Clave:** Ángulo Ve–Vi = 5.4° vs Ángulo S–Ve = 22.4°. Versicolor y Virginica tienen casi la misma dirección geométrica.

---

### Tema 09 | Ortogonalidad (Direcciones sin solapamiento)

**🌸 Dummies**
Dos vectores son *ortogonales* cuando su producto escalar es cero: no comparten "información de dirección". La ortogonalidad es la base del PCA: buscamos ejes mutuamente ortogonales para capturar variaciones genuinamente nuevas.

**∑ Algebraico**
$u \perp v \iff \langle u, v \rangle = 0$.
Complemento ortogonal: $W^\perp = \{ v \in V : \langle v, w \rangle = 0 \ \forall w \in W \}$.
$V = W \oplus W^\perp$ y $\dim(W) + \dim(W^\perp) = \dim(V)$.
Conjunto ortonormal: $\{u_i\}$ es ortonormal $\iff \langle u_i, u_j \rangle = \delta_{ij}$ (delta de Kronecker).

**🔢 Cálculo con el Iris**
Construyendo un vector ortogonal a $\mu_s$:
Buscamos $v \in \mathbb{R}^4$ tal que $\langle \mu_s, v \rangle = 0$:
$$5.006 v_1 + 3.428 v_2 + 1.462 v_3 + 0.246 v_4 = 0$$
Fijamos $v_2 = 1, v_3 = v_4 = 0 \implies v_1 = -3.428 / 5.006 = -0.685$.
$v = [-0.685, 1, 0, 0]^T$. $\langle \mu_s, v \rangle = -3.429 + 3.428 = -0.001 \approx 0$ (✓).
$\dim(\text{span}\{\mu_s\}^\perp) = 4 - 1 = 3$. Hay una familia 3D de "correcciones" ciegas a la media de Setosa.

---

### Tema 10 | Proceso de Gram-Schmidt (Ortonormalización de las especies)

**🌸 Dummies**
Gram-Schmidt toma un conjunto LI y los convierte en vectores *ortonormales* (perpendiculares y de longitud 1). El segundo vector se "limpia" de su componente en la dirección del primero, y así sucesivamente. Construimos coordenadas perfectamente ortogonales a partir de las 3 flores-media.

**∑ Algebraico**
Algoritmo para $\{v_1, v_2, v_3\}$:
* Paso 1: $u_1 = \frac{v_1}{\|v_1\|}$
* Paso 2: $w_2 = v_2 - \langle v_2, u_1 \rangle u_1 \implies u_2 = \frac{w_2}{\|w_2\|}$
* Paso 3: $w_3 = v_3 - \langle v_3, u_1 \rangle u_1 - \langle v_3, u_2 \rangle u_2 \implies u_3 = \frac{w_3}{\|w_3\|}$

**🔢 Cálculo con el Iris (sobre $\{\mu_s, \mu_{ve}, \mu_{vi}\}$)**
Paso 1: Normalizar $\mu_s$ ($\|\mu_s\| = 6.246$).
$$u_1 = \frac{\mu_s}{6.246} = [0.8015, 0.5488, 0.2341, 0.0394]^T$$

Paso 2: Ortogonalizar $\mu_{ve}$ respecto a $u_1$:
$$\langle \mu_{ve}, u_1 \rangle = 5.936(0.8015) + 2.770(0.5488) + 4.260(0.2341) + 1.326(0.0394) = 7.327$$
$$w_2 = \mu_{ve} - 7.327 u_1 = [5.936, 2.770, 4.260, 1.326] - [5.872, 4.022, 1.715, 0.289]$$
$$w_2 = [0.064, -1.252, 2.545, 1.037]^T$$
$\|w_2\| = \sqrt{0.004 + 1.568 + 6.477 + 1.075} = 3.021$.
$$u_2 = \frac{w_2}{3.021} = [0.0212, -0.4143, 0.8426, 0.3432]^T$$
Verificación: $\langle u_1, u_2 \rangle = 0.017 - 0.227 + 0.197 + 0.014 = 0.001 \approx 0$ (✓).

---

## 📦 BLOQUE III: MATRICES

### Tema 11 | Transformaciones Lineales

**🌸 Dummies**
Una *transformación lineal* es una función que "respeta las operaciones": suma y escalar. Seleccionar sólo las variables de pétalo, o centrar los datos restando la media, son transformaciones.

**∑ Algebraico**
$T: V \to W$ es lineal $\iff T(\alpha u + \beta v) = \alpha T(u) + \beta T(v)$.
$\ker(T) = \{ v \in V : T(v) = \mathbf{0} \}$ (núcleo).
$\text{Im}(T) = \{ T(v) : v \in V \}$ (imagen).
Teorema rango-nulidad: $\dim(\ker T) + \dim(\text{Im } T) = \dim(V)$.

**🔢 Cálculo con el Iris**
$T: \mathbb{R}^4 \to \mathbb{R}^2$ — proyección sobre pétalos: $T([x_1, x_2, x_3, x_4]^T) = [x_3, x_4]^T$.
Matriz de $T$ ($2 \times 4$):
$$A = \begin{bmatrix} 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$$
Aplicando a las medias:
$T(\mu_s) = [1.462, 0.246]^T$
$T(\mu_{ve}) = [4.260, 1.326]^T$
$\ker(T) = \{[x_1, x_2, 0, 0]^T\} \implies \dim=2$.
$\text{Im}(T) = \mathbb{R}^2 \implies \dim=2$.
$2 + 2 = 4 = \dim(\mathbb{R}^4)$ (✓).

---

### Tema 12 | Representación Matricial

**🌸 Dummies**
Toda transformación lineal se representa como una multiplicación de matrices. La matriz es la "tabla de instrucciones": columna j = dónde va el j-ésimo vector base.

**∑ Algebraico**
$[T]_{ij} =$ i-ésima componente de $T(e_j)$.
$T(v) = [T] \cdot v$.
Cambio de base: $[T]_{B'} = P^{-1}[T]_E P$, donde $P$ es la matriz de cambio de base.
Composición: $[T_2 \circ T_1] = [T_2] \cdot [T_1]$.

**🔢 Cálculo con el Iris**
Transformación "centrado de datos" $T_c: x \mapsto x - \mu_g$. Es una transformación AFÍN, la hacemos lineal con coordenadas homogéneas en $\mathbb{R}^5$:
$$A_c = \begin{bmatrix} 1 & 0 & 0 & 0 & -5.843 \\ 0 & 1 & 0 & 0 & -3.057 \\ 0 & 0 & 1 & 0 & -3.758 \\ 0 & 0 & 0 & 1 & -1.199 \\ 0 & 0 & 0 & 0 & 1 \end{bmatrix}$$
Aplicando a $\mu_s$ aumentada:
$$A_c \cdot \mu_s^{\text{aug}} = [5.006-5.843, 3.428-3.057, 1.462-3.758, 0.246-1.199, 1]^T$$
$$= [-0.837, 0.371, -2.296, -0.953, 1]^T$$
Interpretación: Setosa tiene pétalos MUY por debajo de la media global, y sépalos ligeramente por debajo.

---

### Tema 13 | Rango y Nulidad

**🌸 Dummies**
El *rango* de una matriz es el número de dimensiones independientes que "genera" al actuar sobre vectores: cuánta información genuinamente distinta produce. La *nulidad* es la dimensión del núcleo: lo que se aplana a cero.

**∑ Algebraico**
$\text{rang}(A) = \dim(\text{Im } A)$ (espacio columna).
$\text{nul}(A) = \dim(\ker A)$ (espacio nulo).
Teorema rango-nulidad: $\text{rang}(A) + \text{nul}(A) = n$.
$\text{rang}(A) \leq \min(m,n)$.

**🔢 Cálculo con el Iris**
Matriz de datos Iris $X$ ($9 \text{ flores} \times 4 \text{ variables}$):
$$X = \begin{bmatrix} 5.1 & 3.5 & 1.4 & 0.2 \\ 4.9 & 3.0 & 1.4 & 0.2 \\ \vdots & \vdots & \vdots & \vdots \\ 7.1 & 3.0 & 5.9 & 2.1 \end{bmatrix}$$
Tras eliminación de Gauss sobre las 4 columnas: $\text{rang}(X) = 4$.
Todas las columnas son LI: cada variable morfológica aporta información genuinamente nueva.
$\text{nul}(X^T) = 4 - 4 = 0$. Rango-nulidad sobre $X$: $4 + 0 = 4$ (✓).

---

### Tema 14 | Cambio de Base

**🌸 Dummies**
Un cambio de base es medir las flores con un sistema de coordenadas diferente. La flor no cambia, pero sus números sí.

**∑ Algebraico**
$[v]_E = P \cdot [v]_B$, $[v]_B = P^{-1} \cdot [v]_E$, donde $P = [b_1|b_2|\dots|b_n]$.
Matrices semejantes: $[T]_B = P^{-1} [T]_E P$ (tienen los mismos eigenvalores).

**🔢 Cálculo con el Iris**
Cambio a base orientada a la "flor media" ($b_1 = \mu_g$):
$\|\mu_g\| = 7.685$.
$b_1 = \frac{\mu_g}{7.685} = [0.7603, 0.3978, 0.4890, 0.1560]^T$
Coordenada de cada media en la dirección $b_1$:
$[\mu_s]_{b_1} = \langle \mu_s, b_1 \rangle = 3.807 + 1.364 + 0.715 + 0.038 = 5.924$
$[\mu_{ve}]_{b_1} = \langle \mu_{ve}, b_1 \rangle = 4.514 + 1.102 + 2.083 + 0.207 = 7.906$
$[\mu_{vi}]_{b_1} = \langle \mu_{vi}, b_1 \rangle = 5.009 + 1.183 + 2.715 + 0.316 = 9.223$
En la dirección "flor media": Setosa < Versicolor < Virginica.

---

### Tema 15 | Determinante

**🌸 Dummies**
El *determinante* mide el factor de escala de volumen de la transformación. Si $\det=0$, la transformación "aplana" alguna dimensión y no es invertible. Para la matriz de covarianza del Iris: si $\det>0$, es invertible y podemos usarla en la distancia de Mahalanobis.

**∑ Algebraico**
$\det(AB) = \det(A)\det(B)$.
$\det(A^T) = \det(A)$.
$\det(\alpha A) = \alpha^n \det(A)$.
$A$ invertible $\iff \det(A) \neq 0$.

**🔢 Cálculo con el Iris**
$\det(\Sigma_{pooled})$ — covarianza pooled del Iris:
$$\Sigma_{pooled} = \begin{bmatrix} 0.265 & 0.093 & 0.168 & 0.038 \\ 0.093 & 0.115 & 0.055 & 0.033 \\ 0.168 & 0.055 & 0.186 & 0.042 \\ 0.038 & 0.033 & 0.042 & 0.043 \end{bmatrix}$$
Descomposición LU — pivotes de la diagonal de U:
$d_1 = 0.2650$
$d_2 = 0.0218 / 0.265 = 0.0823$
$d_3 = 0.00173 / 0.0218 = 0.0793$
$d_4 = 2.41\times10^{-5} / 0.00173 = 0.0139$
$\det(\Sigma_{pooled}) = 0.2650 \times 0.0823 \times 0.0793 \times 0.0139 \approx 2.41 \times 10^{-5}$
> **🔑 Clave:** $\det > 0 \implies \Sigma_{pooled}$ es invertible. Un determinante tan pequeño indica que las variables están bastante correlacionadas (el "hipervolumen" del elipsoide de confianza es muy pequeño).
