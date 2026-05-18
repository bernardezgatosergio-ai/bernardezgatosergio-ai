# 📙 Cuadernillo III — Álgebra sobre Iris (Temas 16–30)

Aplicación Práctica · Eigenvalores y diagonalización, formas bilineales y cuadráticas, criterio de Sylvester, Jacobiano, Hessiano, espacio dual y tensores — todo sobre el Iris real de Fisher (1936).

---

## 📦 BLOQUE IV: EIGENVALORES

### Tema 16 | Valores y Vectores Propios (Las direcciones invariantes)

**🌸 Dummies**
Un *vector propio* de una transformación es una dirección que no se rota al aplicarla — sólo se estira o comprime. El factor de estiramiento es el *valor propio* (eigenvalor). Para la covarianza del Iris: los vectores propios son exactamente las direcciones del PCA. El mayor eigenvalor corresponde a la dirección en que las flores varían más.

**∑ Algebraico**
Ecuación de eigenvalores:
$$A \cdot v = \lambda \cdot v, \quad v \neq 0$$
Reescribiendo: $(A - \lambda I)v = \mathbf{0} \iff \det(A - \lambda I) = 0$ (polinomio característico).
Relaciones espectro $\leftrightarrow$ invariantes matriciales:
$$\text{tr}(A) = \sum_i \lambda_i$$
$$\det(A) = \prod_i \lambda_i$$

**🔢 Cálculo con el Iris — $\Sigma_{\text{total}}$ real**
Matriz de covarianza total (150 flores):
$$\Sigma_{\text{total}} = \begin{bmatrix} 0.6857 & -0.0424 & 1.2743 & 0.5163 \\ -0.0424 & 0.1900 & -0.3297 & -0.1216 \\ 1.2743 & -0.3297 & 3.1163 & 1.2956 \\ 0.5163 & -0.1216 & 1.2956 & 0.5810 \end{bmatrix}$$
Eigenvalores:
* $\lambda_1 = 4.2282$ (PC1, captura 92.46% de varianza)
* $\lambda_2 = 0.2427$ (PC2, captura 5.31%)
* $\lambda_3 = 0.0782$ (PC3, captura 1.71%)
* $\lambda_4 = 0.0237$ (PC4, captura 0.52%)

Verificación:
$\sum \lambda_i = 4.5728 \approx \text{tr}(\Sigma) = 4.5730$ (✓)
$\prod \lambda_i = 0.001899 \approx \det(\Sigma)$ (✓)
> **🔑 Conclusión:** Un solo eigenvalor ($\lambda_1$) captura el 92% de la varianza. El espectro confirma que los datos del Iris son esencialmente unidimensionales.

---

### Tema 17 | Diagonalización (La forma más simple de la covarianza)

**🌸 Dummies**
*Diagonalizar* una matriz es encontrar una base en la que la transformación sea simple: sólo estira/comprime. En esa base, la matriz es diagonal. Para la covarianza del Iris: equivale a encontrar los ejes del PCA, donde las 4 variables nuevas son completamente no correlacionadas.

**∑ Algebraico**
Descomposición espectral (Teorema Espectral para matrices simétricas):
$$A = Q \cdot \Lambda \cdot Q^T$$
$Q \in \mathbb{R}^{n \times n}$ ortogonal (columnas = eigenvectores ortonormales).
$\Lambda = \text{diag}(\lambda_1, \dots, \lambda_n)$.
Suma de matrices de rango 1: $A = \sum_i \lambda_i q_i q_i^T$.

**🔢 Cálculo con el Iris**
Eigenvectores reales (columnas de $Q$):
$q_1 = [0.3614, -0.0845, 0.8567, 0.3583]^T$
$q_2 = [0.6566, 0.7302, -0.1734, -0.0755]^T$
$q_3 = [-0.5820, 0.5970, 0.0762, 0.5459]^T$
$q_4 = [0.3155, -0.3197, -0.4798, 0.7537]^T$

$q_1$ está dominado por longitud de pétalo (0.857) $\to$ es básicamente "tamaño del pétalo".
Verificación $A q_1 = \lambda_1 q_1$:
$(\Sigma \cdot q_1)_1 = 1.529 \approx \lambda_1 \cdot (q_1)_1 = 1.528$ (✓).
Aproximación rango 1: $\Sigma \approx 4.228 q_1 q_1^T$ captura el 92.46%.

---

### Tema 18 | Polinomio Característico (La ecuación secular)

**🌸 Dummies**
El *polinomio característico* es $\det(A-\lambda I)$: un polinomio de grado $n$ cuyas raíces son los eigenvalores. Es invariante al cambio de base.

**∑ Algebraico**
$$p(\lambda) = \det(A-\lambda I) = (-\lambda)^n + c_{n-1}\lambda^{n-1} + \dots + c_0$$
Para $n=4$:
$c_3 = -\text{tr}(A)$
$c_2 = \sum_{i<j} \det(A_{ij})$ (suma de menores $2 \times 2$ principales)
$c_1 = -\sum \det(A_{3 \times 3 \text{ principales}})$
$c_0 = \det(A)$
Teorema de Cayley-Hamilton: $p(A) = 0$.

**🔢 Cálculo con el Iris**
Coeficientes de $p(\lambda)$ para $\Sigma_{\text{total}}$:
$c_3 = -4.5730$
$c_2 = 0.1285 + 0.5133 + 0.1318 + 0.4834 + 0.0956 + 0.1320 = 1.4846$
$c_0 = 0.001899$
$p(\lambda) = \lambda^4 - 4.573\lambda^3 + 1.485\lambda^2 - c_1\lambda + 0.0019$
Sus raíces son exactamente los 4 eigenvalores obtenidos en el Tema 16.

---

### Tema 19 | Matrices Ortogonales (Las rotaciones del espacio Iris)

**🌸 Dummies**
Una *matriz ortogonal* $Q$ representa una rotación (o reflexión) pura. Conserva todas las distancias y ángulos. La matriz $Q$ del PCA rota el espacio de las 4 medidas al espacio de componentes principales.

**∑ Algebraico**
$Q \in O(n) \iff Q^T Q = Q Q^T = I$.
Equivalencias: sus columnas forman una base ortonormal; preserva producto escalar $\langle Qu, Qv \rangle = \langle u, v \rangle$; es isometría $\|Qv\| = \|v\|$.
$\det(Q) = \pm 1$ ($+1$ rotación pura, $-1$ reflexión). $Q^{-1} = Q^T$.

**🔢 Cálculo con el Iris**
Verificando $Q = [q_1|q_2|q_3|q_4]$ del Tema 17:
$\|q_1\|^2 = 0.3614^2 + (-0.0845)^2 + 0.8567^2 + 0.3583^2 = 1.0000$ (✓)
$\langle q_1, q_2 \rangle = 0.0002 \approx 0$ (✓)
$\det(Q) = +1.000$ (rotación pura).
Isometría: $\|Q\mu_s\| = \|\mu_s\| = 6.246$.
> **🔑 Clave:** El PCA es una rotación ortogonal. La información se conserva íntegramente; sólo cambia el sistema de coordenadas.

---

## 📦 BLOQUE V: FORMAS

### Tema 20 | Formas Bilineales (Funciones lineales en dos argumentos)

**🌸 Dummies**
Una *forma bilineal* toma dos vectores y devuelve un número, siendo lineal en cada argumento. La forma $B(u,v) = u^T \Sigma v$ mide "cuánto covarian $u$ y $v$ bajo la distribución de las flores".

**∑ Algebraico**
$B(u,v) = u^T [B] v$.
Toda forma bilineal se descompone en parte simétrica y antisimétrica: $B = \frac{1}{2}(B+B^T) + \frac{1}{2}(B-B^T)$.

**🔢 Cálculo con el Iris**
Evaluando $B(\mu_s, \mu_{ve}) = \mu_s^T \Sigma_{\text{pooled}} \mu_{ve}$:
Paso 1: $w = \Sigma_{\text{pooled}} \cdot \mu_{ve} = [2.597, 1.149, 1.997, 0.553]^T$
Paso 2: $B(\mu_s, \mu_{ve}) = \mu_s^T w = 19.995$
Verificar simetría: $B(\mu_{ve}, \mu_s) = \mu_{ve}^T \Sigma \mu_s = 19.995$ (✓).

---

### Tema 21 | Formas Cuadráticas (La geometría de la varianza)

**🌸 Dummies**
Evalúa una forma bilineal simétrica en el mismo vector: $Q(v) = v^T A v$. Para el Iris, $Q(v) = v^T \Sigma v$ nos dice "cuánta varianza tiene la dirección $v$". Es el centro de la distancia de Mahalanobis.

**∑ Algebraico**
Definida positiva: $Q(v) > 0 \ \forall v \neq 0 \iff \lambda_i > 0 \ \forall i$.
Forma canónica: $Q(y) = \lambda_1 y_1^2 + \dots + \lambda_n y_n^2$.

**🔢 Cálculo con el Iris**
Evaluando $Q(d) = d^T \Sigma_{\text{pooled}} d$ para $d = \mu_{ve} - \mu_s = [0.930, -0.658, 2.798, 1.080]^T$:
$\Sigma d = [0.696, 0.201, 0.685, 0.177]^T$
$Q(d) = d^T (\Sigma d) = 2.623 > 0$ (✓, confirma que $\Sigma$ es def. positiva).
$\sqrt{Q(d)} = 1.620$ es la distancia de Mahalanobis entre Setosa y Versicolor.

---

### Tema 22 | Criterio de Sylvester (Cuándo es positiva definida la covarianza)

**🌸 Dummies**
Permite verificar si $Q(v)$ es definida positiva sin calcular todos los eigenvalores. Basta comprobar que los *menores principales líderes* son todos positivos.

**∑ Algebraico**
$A \in \mathbb{R}^{n \times n}$ simétrica es definida positiva $\iff \Delta_k > 0 \ \forall k=1,\dots,n$, donde $\Delta_k$ es el determinante de la submatriz superior izquierda de $k \times k$.

**🔢 Cálculo con el Iris**
Sobre $\Sigma_{\text{pooled}}$:
$\Delta_1 = 0.265 > 0$
$\Delta_2 = \det \begin{bmatrix} 0.265 & 0.093 \\ 0.093 & 0.115 \end{bmatrix} = 0.0218 > 0$
$\Delta_3 \approx 0.00173 > 0$
$\Delta_4 = \det(\Sigma) \approx 2.41 \times 10^{-5} > 0$
> **🔑 Conclusión:** $\Sigma_{\text{pooled}}$ es definida positiva. Garantiza que la distancia de Mahalanobis está bien definida.

---

### Tema 23 | Traza y Norma de Frobenius (El tamaño total)

**🌸 Dummies**
La *traza* es la varianza total (suma de varianzas individuales). La *norma de Frobenius* mide el "tamaño total" de la matriz.

**∑ Algebraico**
$\text{tr}(A) = \sum a_{ii} = \sum \lambda_i$.
$\|A\|_F = \sqrt{\sum_{i,j} a_{ij}^2} = \sqrt{\text{tr}(A^T A)} = \sqrt{\sum \sigma_i^2}$. Para simétricas: $\|A\|_F = \sqrt{\sum \lambda_i^2}$.

**🔢 Cálculo con el Iris**
$\text{tr}(\Sigma_{\text{total}}) = 4.5730$. Desglose: sep.len (15%), sep.wid (4.2%), pet.len (68.1%), pet.wid (12.7%).
$\|\Sigma_{\text{total}}\|_F = \sqrt{17.944} = 4.236$.
Verificación con eigenvalores: $\sum \lambda_i^2 = 4.228^2 + \dots \approx 17.942$ (✓).

---

## 📦 BLOQUE VI: ANÁLISIS

### Tema 24 | Gradiente y Diferencial (La dirección de máxima variación)

**🌸 Dummies**
El *gradiente* apunta en la dirección de mayor crecimiento. La diferencial es la mejor aproximación lineal local.

**∑ Algebraico**
$\nabla f(x) = [\frac{\partial f}{\partial x_1}, \dots, \frac{\partial f}{\partial x_n}]^T$.
$df_x(h) = \nabla f(x)^T h$.
Si $A$ es simétrica: $\nabla (x^T A x) = 2Ax$.

**🔢 Cálculo con el Iris**
Gradiente de la log-densidad gaussiana de Setosa evaluada en $\mu_{ve}$:
$\ell_s(x) = -\frac{1}{2}(x-\mu_s)^T \Sigma^{-1} (x-\mu_s)$
$\nabla \ell_s(x) = -\Sigma^{-1}(x-\mu_s)$
$\nabla \ell_s(\mu_{ve}) \approx -[-6.113, 3.542, 22.134, -19.877]^T = [6.113, -3.542, -22.134, 19.877]^T$
> **🔑 Conclusión:** "Para que Versicolor sea más parecida a Setosa, principalmente hay que reducir longitud pétalo (-22.1) y aumentar ancho pétalo (+19.9)".

---

### Tema 25 | Jacobiano (La derivada vectorial)

**🌸 Dummies**
El *Jacobiano* generaliza el gradiente de $\mathbb{R}^n \to \mathbb{R}^m$. La fila $i$ es el gradiente de la función $i$.

**∑ Algebraico**
$[J_f]_{ij} = \frac{\partial f_i}{\partial x_j}$. Regla cadena: $J_{g \circ f}(x) = J_g(f(x)) \cdot J_f(x)$.

**🔢 Cálculo con el Iris**
Jacobiano de softmax $g(s)$ en $\mu_s$:
$J_g(s) = \text{diag}(g) - g g^T$. Si $g = [0.97, 0.02, 0.01]^T$:
$J_g = \begin{bmatrix} 0.029 & -0.019 & -0.010 \\ -0.019 & 0.020 & 0.000 \\ -0.010 & 0.000 & 0.010 \end{bmatrix}$
Setosa está "saturada": mover la flor poco apenas cambia la predicción.

---

### Tema 26 | Hessiano (La curvatura)

**🌸 Dummies**
Matriz de segundas derivadas. Mide curvatura. Si es definido positivo, hay un mínimo local.

**∑ Algebraico**
$H(f) = [\frac{\partial^2 f}{\partial x_i \partial x_j}]$. Simétrica si $f \in C^2$.

**🔢 Cálculo con el Iris**
$g(x) = (x-\mu_s)^T \Sigma^{-1} (x-\mu_s)$ (Mahalanobis²).
$\nabla g = 2\Sigma^{-1}(x-\mu_s) \implies H(g) = 2\Sigma^{-1}$.
Eigenvalores de $H(g) = 2/\lambda_i(\Sigma)$: $[5.56, 14.8, 24.4, 62.5]$.
Mayor curvatura en direcciones de menor varianza (la distancia Mahalanobis estira las direcciones más sensibles).

---

## 📦 BLOQUE VII: ESPACIO DUAL

### Tema 27 | Espacio Dual (Funcionales)

**🌸 Dummies**
$V^*$ es el espacio de funciones lineales de $V \to \mathbb{R}$. Los elementos del dual son "medidores".

**∑ Algebraico**
$\dim(V^*) = \dim(V)$. Base dual: $e^i(e_j) = \delta_{ij}$. $\varphi(v) = \sum \varphi_i v_i = \varphi^T v$.

**🔢 Cálculo con el Iris**
Funcional "índice pétalo total": $\varphi_{pet} = e^3 + e^4$.
$\varphi_{pet}(\mu_s) = 1.462 + 0.246 = 1.708$
$\varphi_{pet}(\mu_{ve}) = 5.586$
$\varphi_{pet}(\mu_{vi}) = 7.578$
¡Separa perfectamente las 3 especies!

---

### Tema 28 | Base Dual y Aniquilador (Lo que no miden los funcionales)

**🌸 Dummies**
El aniquilador de $W$ son los funcionales del dual que dan 0 sobre $W$. Son "medidores ciegos" a $W$.

**∑ Algebraico**
$W^0 = \{ \varphi \in V^* : \varphi(w) = 0 \ \forall w \in W \}$.
$\dim(W^0) = \dim(V) - \dim(W)$.

**🔢 Cálculo con el Iris**
Aniquilador de $\text{span}\{\mu_s\}$: funcionales $\varphi$ tal que $5.006\varphi_1 + \dots = 0$. $\dim = 3$.
Un vector base de $W^0$: $\varphi_1 = (-0.685, 1, 0, 0)$.
$\varphi_1(\mu_s) \approx 0$ (✓). $\varphi_1(\mu_{ve}) = -1.296$. $\varphi_1$ distingue Versicolor aunque sea ciego a Setosa.

---

## 📦 BLOQUE VIII: TENSORES

### Tema 29 | Producto Tensorial (Combinando espacios)

**🌸 Dummies**
$V \otimes W$ captura interacciones pareadas. $\Sigma$ es un tensor de rango (0,2) en $V^* \otimes V^*$.

**∑ Algebraico**
Tipos de tensor (p,q): $p$ contravariantes (arriba), $q$ covariantes (abajo).
Vector (1,0); Funcional (0,1); Covarianza (0,2).

**🔢 Cálculo con el Iris**
Correlaciones a partir del tensor $\Sigma$:
$r_{34} = 1.2956 / \sqrt{3.1163 \cdot 0.5810} = 0.963$ (pétalos: casi perfecta).
$r_{23} = -0.428$ (ancho sépalo y longitud pétalo: negativa).

---

### Tema 30 | Transformación Tensorial (Cambio de base)

**🌸 Dummies**
Si cambiamos centímetros a milímetros en pétalos, la covarianza se transforma de forma covariante.

**∑ Algebraico**
Tensor (0,2): $\Sigma'_{ab} = P^i_a P^j_b \Sigma_{ij} \implies \Sigma' = P^T \Sigma P$.

**🔢 Cálculo con el Iris**
$P = \text{diag}(1, 1, 10, 10)$.
$\Sigma'_{33} = 10 \cdot 10 \cdot 3.116 = 311.6$ (×100).
Verificando correlación invariante: $r'_{34} = 129.6 / \sqrt{311.6 \cdot 58.1} = 0.963 = r_{34}$ original.
> **🔑 Conclusión:** Las invariantes geométricas son independientes de las unidades.
