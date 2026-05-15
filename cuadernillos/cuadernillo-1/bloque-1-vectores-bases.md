# 📐 Cuadernillo I — Bloque I
## El Espacio de los Datos: Vectores y Bases

> *"Si el sistema no fuera un espacio vectorial, el concepto de combinación de características sería imposible."*

[⬅️ Volver al Índice Maestro](../README.md)

---

## Capítulo 1 — El Axioma de Espacio Vectorial sobre ℝ

### Explicación Intuitiva: El lienzo infinito
Imagina una rejilla de píxeles. Un Espacio Vectorial funciona como un reglamento de juego consistente: si sumamos dos imágenes o escalamos una, el resultado permanece dentro del mismo lienzo. Es la garantía de que podemos operar con la realidad — imágenes, sonidos, textos — sin que la estructura matemática se rompa. Sin este reglamento, no podríamos sumar fuerzas en física ni ajustar pesos en una red neuronal.

### Ejemplo Aplicado: El Espacio de Intensidades
Cada configuración de imagen es un vector. Sobre ℝ realizamos dos operaciones críticas:
* **Suma (u + v):** Superposición de imágenes — el resultado reside en el mismo espacio.
* **Producto escalar (λ·v):** Si multiplicamos por 0.5, reducimos el brillo a la mitad.

**Relación con la IA:** Cuando una red neuronal mezcla información de diferentes neuronas para detectar una forma, está realizando exactamente estas operaciones.

### Rigor Matemático
Sea V un conjunto no vacío y ℝ el cuerpo de reales. V es un **espacio vectorial** si cumple para todo u, v, w ∈ V y λ, μ ∈ ℝ:

| Propiedad | Expresión |
|-----------|-----------|
| Asociatividad | (u + v) + w = u + (v + w) |
| Conmutatividad | u + v = v + u |
| Elemento neutro | ∃ 0 ∈ V tal que v + 0 = v |
| Elemento opuesto | ∃ (-v) tal que v + (-v) = 0 |
| Distributividad (vectores) | λ(u + v) = λu + λv |
| Distributividad (escalares) | (λ + μ)v = λv + μv |
| Compatibilidad | λ(μv) = (λμ)v |
| Elemento unidad | 1·v = v |

**Justificación:** Usamos ℝ y no ℤ porque el aprendizaje automático requiere continuidad. Los reales permiten correcciones infinitesimales de gradiente — un viaje suave por una superficie infinita de posibilidades.

### Figuras

<details>
<summary><b>🖼️ Figura 1.1 — Clausura vectorial</b></summary>
<br>
<img src="../img/bloque-1/fig-01-1-clausura.png" width="100%">
<p><em>Dos rejillas de píxeles entran en la operación suma y sale una tercera rejilla del mismo tamaño — la clausura garantiza que no salimos del espacio.</em></p>
</details>

<details>
<summary><b>🖼️ Figura 1.2 — Escalado de imagen</b></summary>
<br>
<img src="../img/bloque-1/fig-01-2-escalado.png" width="100%">
<p><em>Una imagen que se desvanece al multiplicarse por 0.1 y se satura al multiplicarse por 2.</em></p>
</details>

<details>
<summary><b>🖼️ Figura 1.3 — Suma geométrica (regla del paralelogramo)</b></summary>
<br>
<img src="../img/bloque-1/fig-01-3-suma-geometrica.png" width="100%">
<p><em>Dos vectores u y v sumados mediante la regla del paralelogramo — la suma de imágenes es, en el fondo, una suma de flechas en el hiperespacio.</em></p>
</details>

---

## Capítulo 2 — El Píxel como Dimensión: El Espacio de Intensidades Vⁿ

### Explicación Intuitiva: El mundo de muchas direcciones
Para una IA, cada dato independiente es una nueva dirección. Una foto de 1 megapíxel se visualiza en un espacio con un millón de ejes independientes — permite que la IA separe cosas que en 2D parecen mezcladas.

### Ejemplo Aplicado: De la cuadrícula al vector
Una imagen de 9 píxeles se representa como:

$$v = (v_1, v_2, v_3, v_4, v_5, v_6, v_7, v_8, v_9) \in \mathbb{R}^9$$

En LLMs, una palabra se representa con hasta 4096 dimensiones — cada una captura un concepto abstracto diferente.

### Rigor Matemático
Un vector v ∈ ℝⁿ es una secuencia finita de reales. Para que cada píxel sea una dimensión real, los vectores base deben ser linealmente independientes:

$$\alpha_1 e_1 + \alpha_2 e_2 + \dots + \alpha_n e_n = 0 \implies \alpha_1 = \alpha_2 = \dots = \alpha_n = 0$$

Esta independencia garantiza que no perdemos información al aplanar la imagen en un vector.

### Figuras

<details>
<summary><b>🖼️ Figura 2.1 — Flattening: de matriz a vector</b></summary>
<br>
<img src="../img/bloque-1/fig-02-1-flattening.png" width="100%">
<p><em>Una matriz 3×3 que se estira para convertirse en un vector columna de ℝ⁹.</em></p>
</details>

<details>
<summary><b>🖼️ Figura 2.2 — Proyección 2D vs 3D</b></summary>
<br>
<img src="../img/bloque-1/fig-02-2-proyeccion-2d-3d.png" width="100%">
<p><em>Dos puntos que se solapan en 2D se separan claramente al añadir una tercera dimensión.</em></p>
</details>

<details>
<summary><b>🖼️ Figura 2.3 — El Hiperespacio</b></summary>
<br>
<img src="../img/bloque-1/fig-02-3-hiperespacio.png" width="100%">
<p><em>Sistema de coordenadas con 3 ejes etiquetados con posiciones de píxel — un vector como punto único en el espacio.</em></p>
</details>

---

## Capítulo 3 — Independencia Lineal: La Pureza de la Información

### Explicación Intuitiva: El mensajero que no aporta nada
La independencia lineal garantiza que cada neurona aporta información única. Si un píxel puede deducirse de otros, es redundante — es ruido que la IA debe eliminar.

### Ejemplo Aplicado: La redundancia en la rejilla
Si el píxel 3 siempre es la suma del 1 y el 2:

$$e_3 = e_1 + e_2 \implies e_3 \text{ es linealmente dependiente}$$

La red se vuelve inestable cuando hay correlación perfecta entre variables.

### Rigor Matemático
{v₁, ..., vₖ} son Linealmente Independientes (L.I.) si:

$$\alpha_1 v_1 + \alpha_2 v_2 + \dots + \alpha_k v_k = 0 \implies \alpha_1 = \alpha_2 = \dots = \alpha_k = 0$$

El rango de las matrices de pesos determina la capacidad real de aprendizaje — filas dependientes colapsan dimensiones y destruyen información.

### Figuras

<details>
<summary><b>🖼️ Figura 3.1 — Dependencia vs Independencia</b></summary>
<br>
<img src="../img/bloque-1/fig-03-1-dependencia.png" width="100%">
<p><em>Dos flechas sobrepuestas (dependientes) frente a dos flechas en distintas direcciones (independientes).</em></p>
</details>

<details>
<summary><b>🖼️ Figura 3.2 — La sombra</b></summary>
<br>
<img src="../img/bloque-1/fig-03-2-sombra.png" width="100%">
<p><em>Un vector que cae dentro del plano generado por otros dos — no aporta nueva altura al espacio.</em></p>
</details>

<details>
<summary><b>🖼️ Figura 3.3 — Redundancia de píxeles</b></summary>
<br>
<img src="../img/bloque-1/fig-03-3-redundancia.png" width="100%">
<p><em>Dos píxeles que siempre se iluminan igual — información redundante marcada como descartable.</em></p>
</details>

---

## Capítulo 4 — Sistemas de Generadores y el Concepto de Base

### Explicación Intuitiva: El kit de construcción definitivo
Una Base es el conjunto mínimo de piezas con el que puedes construir cualquier objeto del espacio. Ni una pieza de más ni una de menos — el equilibrio perfecto entre posibilidad y eficiencia.

### Ejemplo Aplicado: Los 9 átomos del dígito
Los vectores canónicos {e₁, ..., e₉} forman la base de ℝ⁹. El dígito "1" usando los píxeles 2, 5 y 8:

$$v = 1 \cdot e_2 + 1 \cdot e_5 + 1 \cdot e_8$$

En NLP, la dimensión de la base de embeddings determina la riqueza conceptual del modelo.

### Rigor Matemático
B = {b₁, ..., bₙ} es una Base de V si cumple simultáneamente:
1. **Sistema de generadores** — todo v ∈ V se expresa como combinación lineal de B.
2. **Linealmente independiente** — no hay piezas redundantes.

La unicidad de la representación garantiza que cada dato tiene un DNI numérico irrepetible — sin ella, el aprendizaje sería caótico.

### Figuras

<details>
<summary><b>🖼️ Figura 4.1 — Los 9 vectores canónicos</b></summary>
<br>
<img src="../img/bloque-1/fig-04-1-vectores-canonicos.png" width="100%">
<p><em>9 pequeñas imágenes, cada una con un solo píxel blanco etiquetadas e₁ a e₉ — los átomos del espacio.</em></p>
</details>

<details>
<summary><b>🖼️ Figura 4.2 — La receta del dígito</b></summary>
<br>
<img src="../img/bloque-1/fig-04-2-receta-digito.png" width="100%">
<p><em>El número "1" descomponiéndose en la suma de tres vectores base multiplicados por sus intensidades.</em></p>
</details>

<details>
<summary><b>🖼️ Figura 4.3 — El Span</b></summary>
<br>
<img src="../img/bloque-1/fig-04-3-span.png" width="100%">
<p><em>Un plano 2D donde dos vectores base definen el espacio de todas las imágenes posibles de 2 píxeles.</em></p>
</details>

---

## Capítulo 5 — Coordenadas y el Vector como Combinación Lineal

### Explicación Intuitiva: El GPS del Hiperespacio
Las coordenadas son la receta numérica que indica cuánto desplazarse en cada dirección de la base. Como una receta de café — si cambias los números, el resultado es otro café.

### Ejemplo Aplicado: La receta del "1" imperfecto
Un dígito "1" con trazo más débil arriba y abajo:

$$v = 0.6 \cdot e_2 + 1.0 \cdot e_5 + 0.6 \cdot e_8$$
$$[v]_B = (0, 0.6, 0, 0, 1.0, 0, 0, 0.6, 0)$$

Las activaciones de las capas ocultas son coordenadas en espacios de conceptos abstractos.

### Rigor Matemático
Para cualquier v ∈ V con base B = {b₁,...,bₙ}, existe una única combinación:

$$v = \alpha_1 b_1 + \alpha_2 b_2 + \dots + \alpha_n b_n$$

Las coordenadas `[v]_B` son únicas por la independencia lineal de la base. Esta unicidad permite que el software maneje geometría sin ambigüedad.

### Figuras

<details>
<summary><b>🖼️ Figura 5.1 — Suma ponderada</b></summary>
<br>
<img src="../img/bloque-1/fig-05-1-suma-ponderada.png" width="100%">
<p><em>Tres vectores base multiplicados por diferentes transparencias que se fusionan para crear el vector final.</em></p>
</details>

<details>
<summary><b>🖼️ Figura 5.2 — Unicidad del punto</b></summary>
<br>
<img src="../img/bloque-1/fig-05-2-unicidad.png" width="100%">
<p><em>Un punto en espacio 3D con líneas de proyección hacia los ejes — solo un conjunto de valores define su posición.</em></p>
</details>

<details>
<summary><b>🖼️ Figura 5.3 — Vector de activación</b></summary>
<br>
<img src="../img/bloque-1/fig-05-3-activacion.png" width="100%">
<p><em>Una neurona recibiendo múltiples señales (coordenadas) y sumándolas para generar una salida.</em></p>
</details>

---

## Capítulo 6 — Subespacios Vectoriales: Donde Viven las Características

### Explicación Intuitiva: La habitación dentro del palacio
Aunque el palacio tiene un millón de habitaciones, tu vida ocurre en solo tres de ellas. Un Subespacio Vectorial es esa región del espacio total que mantiene las mismas reglas algebraicas.

### Ejemplo Aplicado: El Subespacio de las Líneas Horizontales
Solo los píxeles de la primera fila {e₁, e₂, e₃} forman el subespacio S. Cualquier suma de imágenes de S produce otra imagen de S — la clausura se preserva.

En los Autoencoders, la IA proyecta 784 píxeles en un subespacio de 32 dimensiones — el Latent Space donde viven los datos reales.

### Rigor Matemático
S ⊆ V es un Subespacio Vectorial si y solo si:

| Condición | Expresión |
|-----------|-----------|
| Clausura bajo suma | u, v ∈ S ⟹ u + v ∈ S |
| Clausura bajo escalar | v ∈ S, λ ∈ ℝ ⟹ λv ∈ S |

*Nota: Todo subespacio contiene obligatoriamente el vector nulo (0 ∈ S).*

### Figuras

<details>
<summary><b>🖼️ Figura 6.1 — El Plano en el Espacio</b></summary>
<br>
<img src="../img/bloque-1/fig-06-1-plano-espacio.png" width="100%">
<p><em>Un espacio 3D con un plano coloreado atravesándolo por el origen — vectores sumándose dentro del plano sin poder escapar.</em></p>
</details>

<details>
<summary><b>🖼️ Figura 6.2 — El Filtro de Fila</b></summary>
<br>
<img src="../img/bloque-1/fig-06-2-filtro-fila.png" width="100%">
<p><em>Una rejilla 3×3 donde solo se iluminan los píxeles de la fila superior — miembro del subespacio.</em></p>
</details>

<details>
<summary><b>🖼️ Figura 6.3 — Compresión Latente</b></summary>
<br>
<img src="../img/bloque-1/fig-06-3-compresion-latente.png" width="100%">
<p><em>Un embudo que toma un vector grande y lo proyecta sobre un subespacio de menor dimensión.</em></p>
</details>
