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

```text
v = (v₁, v₂, v₃, v₄, v₅, v₆, v₇, v₈, v₉) ∈ ℝ⁹
En LLMs, una palabra se representa con hasta 4096 dimensiones — cada una captura un concepto abstracto diferente.Rigor MatemáticoUn vector v ∈ ℝⁿ es una secuencia finita de reales. Para que cada píxel sea una dimensión real, los vectores base deben ser linealmente independientes:Plaintextα₁e₁ + α₂e₂ + ... + αₙeₙ = 0  ⟹  α₁ = α₂ = ... = αₙ = 0
Esta independencia garantiza que no perdemos información al aplanar la imagen en un vector.FigurasCapítulo 3 — Independencia Lineal: La Pureza de la InformaciónExplicación Intuitiva: El mensajero que no aporta nadaLa independencia lineal garantiza que cada neurona aporta información única. Si un píxel puede deducirse de otros, es redundante — es ruido que la IA debe eliminar.Ejemplo Aplicado: La redundancia en la rejillaSi el píxel 3 siempre es la suma del 1 y el 2:Plaintexte₃ = e₁ + e₂   →   e₃ es linealmente dependiente
La red se vuelve inestable cuando hay correlación perfecta entre variables.Rigor Matemático{v₁, ..., vₖ} son Linealmente Independientes (L.I.) si:Plaintextα₁v₁ + α₂v₂ + ... + αₖvₖ = 0  ⟹  α₁ = α₂ = ... = αₖ = 0
El rango de las matrices de pesos determina la capacidad real de aprendizaje — filas dependientes colapsan dimensiones y destruyen información.FigurasCapítulo 4 — Sistemas de Generadores y el Concepto de BaseExplicación Intuitiva: El kit de construcción definitivoUna Base es el conjunto mínimo de piezas con el que puedes construir cualquier objeto del espacio. Ni una pieza de más ni una de menos — el equilibrio perfecto entre posibilidad y eficiencia.Ejemplo Aplicado: Los 9 átomos del dígitoLos vectores canónicos {e₁, ..., e₉} forman la base de ℝ⁹. El dígito "1" usando los píxeles 2, 5 y 8:Plaintextv = 1·e₂ + 1·e₅ + 1·e₈
En NLP, la dimensión de la base de embeddings determina la riqueza conceptual del modelo.Rigor MatemáticoB = {b₁, ..., bₙ} es una Base de V si cumple simultáneamente:Sistema de generadores — todo v ∈ V se expresa como combinación lineal de B.Linealmente independiente — no hay piezas redundantes.La unicidad de la representación garantiza que cada dato tiene un DNI numérico irrepetible — sin ella, el aprendizaje sería caótico.FigurasCapítulo 5 — Coordenadas y el Vector como Combinación LinealExplicación Intuitiva: El GPS del HiperespacioLas coordenadas son la receta numérica que indica cuánto desplazarse en cada dirección de la base. Como una receta de café — si cambias los números, el resultado es otro café.Ejemplo Aplicado: La receta del "1" imperfectoUn dígito "1" con trazo más débil arriba y abajo:Plaintextv = 0.6·e₂ + 1.0·e₅ + 0.6·e₈
[v]_B = (0, 0.6, 0, 0, 1.0, 0, 0, 0.6, 0)
Las activaciones de las capas ocultas son coordenadas en espacios de conceptos abstractos.Rigor MatemáticoPara cualquier v ∈ V con base B = {b₁,...,bₙ}, existe una única combinación:Plaintextv = α₁b₁ + α₂b₂ + ... + αₙbₙ
Las coordenadas [v]_B = (α₁,...,αₙ) son únicas por la independencia lineal de la base. Esta unicidad permite que el software maneje geometría sin ambigüedad.FigurasCapítulo 6 — Subespacios Vectoriales: Donde Viven las CaracterísticasExplicación Intuitiva: La habitación dentro del palacioAunque el palacio tiene un millón de habitaciones, tu vida ocurre en solo tres de ellas. Un Subespacio Vectorial es esa región del espacio total que mantiene las mismas reglas algebraicas.Ejemplo Aplicado: El Subespacio de las Líneas HorizontalesSolo los píxeles de la primera fila {e₁, e₂, e₃} forman el subespacio S. Cualquier suma de imágenes de S produce otra imagen de S — la clausura se preserva.En los Autoencoders, la IA proyecta 784 píxeles en un subespacio de 32 dimensiones — el Latent Space donde viven los datos reales.Rigor MatemáticoS ⊆ V es un Subespacio Vectorial si y solo si:CondiciónExpresiónClausura bajo sumau, v ∈ S ⟹ u + v ∈ SClausura bajo escalarv ∈ S, λ ∈ ℝ ⟹ λv ∈ SNota: Todo subespacio contiene obligatoriamente el vector nulo (0 ∈ S).
