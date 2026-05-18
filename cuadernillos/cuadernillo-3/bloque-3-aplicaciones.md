# 📙 Cuadernillo III — Álgebra sobre Iris (Temas 31–45)

Aplicaciones y Síntesis Final · PCA, Mahalanobis, SVD, LDA, hiperplanos, pseudo-inversa, Schur, derivadas matriciales, Riemann — y la síntesis donde todo converge sobre el Iris.

---

## 📦 BLOQUE IX: APLICACIONES

### Tema 31 | PCA — Análisis de Componentes Principales (Comprimiendo el Iris)

**🌸 Dummies**
El PCA encuentra los ejes en que las flores varían más. Con sólo 2 componentes capturamos el 97.77% de la variabilidad de 150 flores en 4 dimensiones. Podemos visualizar el dataset casi perfectamente en 2D.
El PCA *es* la diagonalización de la covarianza: los ejes son los eigenvectores, las varianzas captadas son los eigenvalores. Todo lo de los temas anteriores converge aquí.

**∑ Algebraico**
Algoritmo PCA — pasos algebraicos:
1. Centrar: $X_c = X - \mathbf{1}\cdot\mu^T \quad \text{← restar la media global}$
2. Covarianza: $\Sigma = X_c^T X_c / (n-1) \quad \text{← matriz de covarianza}$
3. Diagonalizar: $\Sigma = Q\Lambda Q^T \quad \text{← Teorema Espectral}$
4. Proyectar: $Z = X_c \cdot Q_k \quad \text{← k componentes}$

Varianza explicada por $PC_i$:
$$VE_i = \frac{\lambda_i}{\sum_j \lambda_j}$$

Reconstrucción de rango $k$ (óptima en $\|\cdot\|_F$):
$$\hat{X} = Z_k \cdot Q_k^T + \mu^T$$
$$\text{Error}_k = \|X - \hat{X}\|_F^2 = \sum_{i>k} \lambda_i$$

**🔢 Cálculo con el Iris**
PCA completo del Iris (150 flores, 4 variables). Eigenvalores y varianza explicada acumulada:
* $\lambda_1 = 4.2282 \to VE_1 = 92.46\% \to \text{acum: } 92.46\%$
* $\lambda_2 = 0.2427 \to VE_2 =  5.31\% \to \text{acum: } 97.77\%$
* $\lambda_3 = 0.0782 \to VE_3 =  1.71\% \to \text{acum: } 99.48\%$
* $\lambda_4 = 0.0237 \to VE_4 =  0.52\% \to \text{acum: } 100.00\%$

PC1 (mayor varianza) — dirección dominante:
$q_1 = [0.3614, -0.0845, 0.8567, 0.3583]^T$
Dominado por longitud pétalo (0.857) $\to$ "tamaño del pétalo".

Proyecciones de las medias sobre PC1 y PC2:
$\mu_s \cdot q_1 = 5.006(0.361) + 3.428(-0.085) + 1.462(0.857) + 0.246(0.358) = 2.858$
$\mu_{ve} \cdot q_1 = 5.936(0.361) + 2.770(-0.085) + 4.260(0.857) + 1.326(0.358) = 6.035$
$\mu_{vi} \cdot q_1 = 6.588(0.361) + 2.974(-0.085) + 5.552(0.857) + 2.026(0.358) = 7.608$

$\mu_s \cdot q_2 = 5.006(0.657) + 3.428(0.730) + 1.462(-0.173) + 0.246(-0.076) = 5.595$
$\mu_{ve} \cdot q_2 = 5.936(0.657) + 2.770(0.730) + 4.260(-0.173) + 1.326(-0.076) = 5.481$
$\mu_{vi} \cdot q_2 = 6.588(0.657) + 2.974(0.730) + 5.552(-0.173) + 2.026(-0.076) = 5.648$

En el plano PC1-PC2:
PC1 separa perfectamente las 3 especies (2.9 vs 6.0 vs 7.6). PC2 apenas diferencia (~5.5 todas) $\to$ sépalo ancho irrelevante. ¡El Iris es esencialmente 1-dimensional!

> **🔑 Conclusión geométrica:** El 92.46% de la variación del Iris está en una sola dirección: el tamaño del pétalo. Las tres especies están perfectamente ordenadas a lo largo de este eje. El dataset 4D es efectivamente 1D.

---

### Tema 32 | Distancia de Mahalanobis (Distancia que respeta la covarianza)

**🌸 Dummies**
La distancia euclídea trata todas las variables por igual. Pero longitud de pétalo varía 10 veces más que ancho de sépalo — una diferencia de 1 cm en el pétalo no es igual de "sorprendente" que en el sépalo.
La *distancia de Mahalanobis* normaliza por la covarianza: mide en unidades de "desviaciones estándar conjuntas". Es la distancia natural cuando hay estructura de covarianza no trivial.

**∑ Algebraico**
Definición y propiedades:
$$d_M(u,v;\Sigma) = \sqrt{(u-v)^T \cdot \Sigma^{-1} \cdot (u-v)}$$
Es una distancia (métrica) si $\Sigma$ es def. positiva. Invariante a transformaciones afines de los datos. $d_M(u,\mu)=1$ define la elipsoide de confianza al nivel $1\sigma$.
Relación con producto interno generalizado: $d_M(u,v)^2 = \|u-v\|_{\Sigma^{-1}}^2 = \langle u-v, u-v \rangle_{\Sigma^{-1}}$.

En coordenadas PCA ($y = Q^T x$): la Mahalanobis es simplemente:
$$d_M(u,v)^2 = \sum_i \frac{(y_i^u - y_i^v)^2}{\lambda_i} \quad \text{← dist. euclídea normalizada por varianza de cada PC}$$

**🔢 Cálculo con el Iris**
$d_M(\mu_s, \mu_{ve})$ bajo $\Sigma_{\text{pooled}}$:
$d = \mu_{ve} - \mu_s = [0.930, -0.658, 2.798, 1.080]^T$

$\Sigma_{\text{pooled}}^{-1}$ (calculada por adjunta/LU):
$$\Sigma^{-1} \approx \begin{bmatrix} 7.20 & -2.30 & -7.82 & 7.00 \\ -2.30 & 9.08 & 2.89 & -9.02 \\ -7.82 & 2.89 & 17.49 & -18.66 \\ 7.00 & -9.02 & -18.66 & 40.14 \end{bmatrix}$$

Paso 1: $w = \Sigma^{-1} \cdot d$
$w_1 = 7.20(0.930) - 2.30(-0.658) - 7.82(2.798) + 7.00(1.080) = 6.696 + 1.513 - 21.882 + 7.560 = -6.113$
$w_2 = -2.30(0.930) + 9.08(-0.658) + 2.89(2.798) - 9.02(1.080) = -2.139 - 5.975 + 8.086 - 9.742 = -9.770$
$w_3 = -7.82(0.930) + 2.89(-0.658) + 17.49(2.798) - 18.66(1.080) = -7.273 - 1.902 + 48.934 - 20.153 = 19.606$
$w_4 = 7.00(0.930) - 9.02(-0.658) - 18.66(2.798) + 40.14(1.080) = 6.510 + 5.935 - 52.231 + 43.351 = 3.565$

Paso 2: $d_M^2 = d^T \cdot w$
$$d_M^2 = 0.930(-6.113) + (-0.658)(-9.770) + 2.798(19.606) + 1.080(3.565)$$
$$= -5.685 + 6.429 + 54.878 + 3.850 = 59.472$$
$$d_M(\mu_s, \mu_{ve}) = \sqrt{59.472} = 7.712$$

Comparar con distancia euclídea (tema 7): $d_E = 3.208$. La Mahalanobis es mayor: normaliza por la alta varianza del pétalo $\to$ la diferencia en pétalo es "sorprendentemente grande".
$d_M(\mu_{ve}, \mu_{vi}) \approx 3.21 \quad \text{← más separadas de lo que parecía}$.

---

### Tema 33 | Descomposición en Valores Singulares (SVD)

**🌸 Dummies**
La SVD descompone *cualquier* matriz (no tiene que ser cuadrada ni simétrica) como producto de tres matrices: una rotación, un estiramiento y otra rotación. Es la generalización más completa de la diagonalización.
Para el Iris: la SVD de la matriz de datos centrada $X_c$ da directamente los componentes principales (columnas de $V$), sus importancias (valores singulares $\sigma_i$) y cómo se proyectan las flores (columnas de $U$).

**∑ Algebraico**
Teorema SVD. Para cualquier $A \in \mathbb{R}^{m \times n}$ con $\text{rang}(A)=r$:
$$A = U \cdot \Sigma_{\text{svd}} \cdot V^T$$
$U \in \mathbb{R}^{m \times m}$ ortogonal $\quad \text{← vectores singulares izquierdos}$
$V \in \mathbb{R}^{n \times n}$ ortogonal $\quad \text{← vectores singulares derechos = PCs}$
$\Sigma_{\text{svd}} = \text{diag}(\sigma_1, \dots, \sigma_r, 0, \dots) \in \mathbb{R}^{m \times n} \ (\sigma_i > 0 \text{ decrecientes})$

Relación con eigenvalores:
$\sigma_i^2 = \lambda_i(A^T A) = \lambda_i(A A^T)$
$V = \text{eigenvectores de } A^T A \quad (= \text{PCs si } A=X_c)$
$U = \text{eigenvectores de } A A^T$

Mejor aproximación rango $k$ (Teorema de Eckart-Young):
$A_k = \sum_{i=1}^k \sigma_i \cdot u_i v_i^T \quad \text{← mínimo error } \|A-A_k\|_F$
$\|A-A_k\|_F^2 = \sum_{i>k} \sigma_i^2$

**🔢 Cálculo con el Iris**
SVD de $X_c$ ($150 \times 4$, datos centrados). Relación $\sigma_i \leftrightarrow \lambda_i(\Sigma)$: $\sigma_i = \sqrt{(n-1)\lambda_i} = \sqrt{149\lambda_i}$.
* $\sigma_1 = \sqrt{149 \cdot 4.2282} = \sqrt{630.0} = 25.10 \quad \text{← PC1}$
* $\sigma_2 = \sqrt{149 \cdot 0.2427} = \sqrt{36.16} =  6.01 \quad \text{← PC2}$
* $\sigma_3 = \sqrt{149 \cdot 0.0782} = \sqrt{11.65} =  3.41 \quad \text{← PC3}$
* $\sigma_4 = \sqrt{149 \cdot 0.0237} = \sqrt{3.531} =  1.88 \quad \text{← PC4}$

Primer vector singular derecho ($= \text{PC1}$, igual que eigenvector de $\Sigma$):
$v_1 = [0.3614, -0.0845, 0.8567, 0.3583]^T$

Energía de la aproximación de rango 1:
$\|X_c\|_F^2 = \sigma_1^2 + \sigma_2^2 + \sigma_3^2 + \sigma_4^2 = 630.0 + 36.2 + 11.7 + 3.5 = 681.4$
$\|X_c - X_{c1}\|_F^2 = \sigma_2^2 + \sigma_3^2 + \sigma_4^2 = 36.2 + 11.7 + 3.5 = 51.4$

Con rango 1 capturamos: $630.0 / 681.4 = 92.46\%$ ✓
Con rango 2: $(630.0 + 36.2) / 681.4 = 97.77\%$ ✓
Reconstrucción rango 1: $\hat{X}_1 = \sigma_1 \cdot u_1 \cdot v_1^T + \mu^T$. Cada flor reconstruida = su proyección sobre PC1 + media global.

---

### Tema 34 | Análisis Discriminante Lineal (LDA)

**🌸 Dummies**
El PCA maximiza la varianza total. El LDA maximiza la *separación entre clases* relativa a la varianza dentro de cada clase. Para el Iris con 3 especies, encuentra hasta 2 ejes discriminantes — y en esos ejes, las tres especies quedan perfectamente separadas.

**∑ Algebraico**
Matrices scatter y criterio de Fisher:
Scatter INTRA-clase (variabilidad dentro de cada especie):
$$S_W = \sum_k \sum_{i \in k} (x_i - \mu_k)(x_i - \mu_k)^T = (n-K)\Sigma_{\text{pooled}}$$
Scatter ENTRE-clases (variabilidad de las medias):
$$S_B = \sum_k n_k(\mu_k - \mu)(\mu_k - \mu)^T$$

Problema generalizado de eigenvalores (criterio de Fisher):
$$S_B \cdot w = \lambda \cdot S_W \cdot w \iff S_W^{-1} S_B w = \lambda w$$
Máximo $K-1$ eigenvalores no nulos ($K = \text{nº clases}$). Para Iris: $K=3 \to 2$ ejes discriminantes (LD1, LD2).
Potencia discriminante: $\lambda_i / \sum \lambda_j$.

**🔢 Cálculo con el Iris**
Matrices scatter del Iris ($n_k = 50$ cada especie):
$\mu_{\text{global}} = [5.843, 3.057, 3.758, 1.199]^T$
$\mu_s - \mu = [-0.837, 0.371, -2.296, -0.953]^T$
$\mu_{ve} - \mu = [0.093, -0.287, 0.502, 0.127]^T$
$\mu_{vi} - \mu = [0.745, -0.083, 1.794, 0.827]^T$

$S_B$ (contribución principal de Setosa, muy alejada):
$S_B = 50(\mu_s-\mu)(\mu_s-\mu)^T + 50(\mu_{ve}-\mu)(\mu_{ve}-\mu)^T + 50(\mu_{vi}-\mu)(\mu_{vi}-\mu)^T$
$S_B[3,3] = 50(-2.296)^2 + 50(0.502)^2 + 50(1.794)^2 = 263.4 + 12.6 + 160.9 = 436.9$

Eigenvalores del problema $S_W^{-1} S_B$ (reales del Iris):
$\lambda_{\text{LD1}} = 32.19 \quad \text{← LD1 captura 99.1\% de separación}$
$\lambda_{\text{LD2}} =  0.29 \quad \text{← LD2 captura  0.9\%}$

Primer discriminante lineal (eje LD1, normalizado):
$w_1 \approx [0.829, 1.534, -2.201, -2.810]^T$

Proyecciones LD1:
$w_1^T \mu_s \approx -7.61$
$w_1^T \mu_{ve} \approx -1.83$
$w_1^T \mu_{vi} \approx  0.95$
Separación LD1 $\gg$ PCA para discriminar: las 3 clases bien separadas.

---

### Tema 35 | Hiperplanos Separadores (La frontera geométrica)

**🌸 Dummies**
Un *hiperplano* en $\mathbb{R}^4$ es una "pared" de 3 dimensiones que divide el espacio en dos mitades. En clasificación, usamos hiperplanos para separar especies: todas las flores a un lado son Setosa, las del otro son Versicolor.
El clasificador bayesiano óptimo coloca la frontera exactamente en el punto medio de Mahalanobis entre las dos medias de clase.

**∑ Algebraico**
Hiperplanos en $\mathbb{R}^n$: $H = \{ x \in \mathbb{R}^n : w^T x + b = 0 \}$.
Distancia de un punto $x_0$ al hiperplano: $d(x_0, H) = |w^T x_0 + b| / \|w\|$.

Frontera bayesiana óptima (gaussianas, $\Sigma$ común). Igualar log-densidades:
$$w = \Sigma^{-1}(\mu_2 - \mu_1)$$
$$b = -\frac{1}{2}(\mu_2 + \mu_1)^T \Sigma^{-1} (\mu_2 - \mu_1) = -\frac{1}{2} w^T (\mu_1 + \mu_2)$$
La frontera pasa por el punto medio de Mahalanobis: $x_{\text{mid}} = \frac{1}{2}(\mu_1 + \mu_2)$ satisface $w^T x_{\text{mid}} + b = 0$ ✓.

**🔢 Cálculo con el Iris**
Hiperplano separador Setosa vs Versicolor:
$w = \Sigma_{\text{pooled}}^{-1}(\mu_{ve} - \mu_s) = [-6.113, -9.770, 19.606, 3.565]^T \quad \text{(del tema 32)}$

Punto medio $\mu_{\text{mid}} = \frac{1}{2}(\mu_s + \mu_{ve}) = [5.471, 3.099, 2.861, 0.786]^T$.
$$b = -w^T \mu_{\text{mid}} = -[(-6.113)(5.471) + (-9.770)(3.099) + 19.606(2.861) + 3.565(0.786)]$$
$$= -[-33.444 - 30.277 + 56.124 + 2.802] = -[-4.795] = 4.795$$

Verificación — el hiperplano clasifica bien las medias:
$w^T \mu_s + b = -30.601 - 33.505 + 28.664 + 0.877 + 4.795 = -29.770 < 0 \to \text{Setosa ✓}$
$w^T \mu_{ve} + b = -36.287 - 27.063 + 83.521 + 4.727 + 4.795 = +29.693 > 0 \to \text{Versicolor ✓}$

Margen de separación = $d_M(\mu_s, \mu_{ve}) = 7.712$. ¡Setosa se clasifica con margen enorme!

---

### Tema 36 | Proyección Ortogonal (La sombra de una flor)

**🌸 Dummies**
La *proyección ortogonal* de un vector sobre un subespacio es el punto más cercano del subespacio a ese vector — su "sombra" perpendicular. La diferencia entre el vector y su proyección es perpendicular al subespacio.
En el Iris: proyectar Virginica sobre el plano generado por $\{u_1, u_2\}$ (del Gram-Schmidt) nos da la "mezcla de Setosa y Versicolor" más parecida a Virginica.

**∑ Algebraico**
Con base ortonormal $\{u_1, \dots, u_k\}$ de $W$:
$$\text{proj}_W(v) = \sum_i \langle v, u_i \rangle u_i$$
Con base general $A = [a_1 | \dots | a_k]$:
$$\text{proj}_W(v) = A(A^T A)^{-1}A^T v = P_W v$$
$P_W = A(A^T A)^{-1}A^T$ es el proyector ortogonal:
$P_W^2 = P_W \quad \text{← idempotente}$
$P_W = P_W^T \quad \text{← simétrico}$
$P_{W^\perp} = I - P_W \quad \text{← proyector sobre el complemento}$
$\text{rang}(P_W) = \dim(W)$.

**🔢 Cálculo con el Iris**
Proyección de $\mu_{vi}$ sobre $\text{span}\{u_1, u_2\}$ (base Gram-Schmidt, tema 10):
$u_1 = [0.8015, 0.5488, 0.2341, 0.0394]^T$
$u_2 = [0.0212, -0.4143, 0.8426, 0.3432]^T$

$\langle \mu_{vi}, u_1 \rangle = 6.588(0.8015) + 2.974(0.5488) + 5.552(0.2341) + 2.026(0.0394) = 5.281 + 1.632 + 1.300 + 0.080 = 8.293$
$\langle \mu_{vi}, u_2 \rangle = 6.588(0.0212) + 2.974(-0.4143) + 5.552(0.8426) + 2.026(0.3432) = 0.140 - 1.232 + 4.677 + 0.695 = 4.280$

$\text{proj}(\mu_{vi}) = 8.293 u_1 + 4.280 u_2 = [6.646, 4.552, 1.943, 0.327] + [0.091, -1.773, 3.606, 1.469] = [6.737, 2.779, 5.549, 1.796]^T$

Componente ortogonal (lo que es "único" en Virginica):
$\mu_{vi} - \text{proj} = [6.588-6.737, 2.974-2.779, 5.552-5.549, 2.026-1.796] = [-0.149, 0.195, 0.003, 0.230]^T$
$\|\text{componente única}\| = \sqrt{0.022 + 0.038 + 0.000 + 0.053} = 0.355$.
Muy pequeña: Virginica casi vive en $\text{span}\{\mu_s, \mu_{ve}\}$ — tiene muy poca información morfológica que no sea combinación de las otras.

---

### Tema 37 | Pseudo-Inversa de Moore-Penrose (Invirtiendo lo no invertible)

**🌸 Dummies**
Cuando una matriz no es cuadrada o no tiene rango completo, no podemos invertirla. La *pseudo-inversa* es la "mejor inversa posible": minimiza el error cuadrático en sistemas sobredeterminados y da la solución de norma mínima en subdeterminados.

**∑ Algebraico**
Pseudo-inversa $A^+$ vía SVD. Si $A = U \Sigma V^T$:
$$A^+ = V \cdot \Sigma^+ \cdot U^T$$
(donde $\Sigma^+ = \text{diag}(1/\sigma_1, \dots, 1/\sigma_r, 0, \dots, 0)$).

Cuatro ecuaciones de Moore-Penrose:
$A A^+ A = A$, $A^+ A A^+ = A^+$, $(A A^+)^T = A A^+$, $(A^+ A)^T = A^+ A$.

Casos especiales:
rang completo columnas: $A^+ = (A^T A)^{-1} A^T \quad \text{← mínimos cuadrados}$
rang completo filas: $A^+ = A^T(A A^T)^{-1} \quad \text{← norma mínima}$
$A$ invertible: $A^+ = A^{-1}$.

**🔢 Cálculo con el Iris**
Regresión mínimos cuadrados: predecir código de especie (1, 2, 3).
Sistema sobredeterminado: $X \cdot \beta = y$ ($X \in \mathbb{R}^{150 \times 4}$, $y = [1,\dots,1, 2,\dots,2, 3,\dots,3]^T$).
Solución: $\hat{\beta} = X^+ y = (X^T X)^{-1} X^T y$.

$X^T X \approx n \Sigma_{\text{total}} + n \mu \mu^T \in \mathbb{R}^{4 \times 4}$ (bien condicionada).
$X^T y \approx n_1 \mu_s + 2n_2 \mu_{ve} + 3n_3 \mu_{vi} = 50\mu_s + 100\mu_{ve} + 150\mu_{vi}$.
$X^T y \approx [50(5.006) + 100(5.936) + 150(6.588), \dots] = [1882.5, \dots]$.

$\hat{\beta}$ estimado (mínimos cuadrados):
$\hat{\beta} \approx [-0.112, -0.040, 0.229, 0.601]^T \quad \text{← pesos}$
$\hat{b} \approx 1.853 \quad \text{← intercept}$

Predicciones en los vectores media:
$\hat{\beta}^T \mu_s + \hat{b} = -0.112(5.006) - 0.040(3.428) + 0.229(1.462) + 0.601(0.246) + 1.853 = -0.561 - 0.137 + 0.335 + 0.148 + 1.853 = 1.638 \approx 1 \quad \text{(Setosa)}$
$\hat{\beta}^T \mu_{ve} + \hat{b} \approx 1.960 \approx 2 \quad \text{(Versicolor)}$
$\hat{\beta}^T \mu_{vi} + \hat{b} \approx 2.921 \approx 3 \quad \text{(Virginica)}$ ✓

---

### Tema 38 | Complemento de Schur (Covarianza condicional)

**🌸 Dummies**
El *complemento de Schur* aparece al invertir matrices en bloques. Para el Iris permite calcular la distribución de unas variables condicionada a otras: si observo el sépalo de una flor, ¿qué predigo sobre sus pétalos? La varianza condicional resultante es siempre menor que la marginal.

**∑ Algebraico**
Complemento de Schur $M/A = D - C A^{-1} B$ para $M = \begin{bmatrix} A & B \\ C & D \end{bmatrix}$.
$\det(M) = \det(A)\det(M/A)$.

En estadística ($x_1, x_2$ gaussianas), $\Sigma = \begin{bmatrix} \Sigma_{11} & \Sigma_{12} \\ \Sigma_{21} & \Sigma_{22} \end{bmatrix}$.
Covarianza condicional de $x_2$ dado $x_1$:
$$\Sigma_{2|1} = \Sigma_{22} - \Sigma_{21} \Sigma_{11}^{-1} \Sigma_{12} \quad \text{← complemento de Schur}$$
Media condicional: $\mu_{2|1}(x_1) = \mu_2 + \Sigma_{21} \Sigma_{11}^{-1} (x_1 - \mu_1)$.

**🔢 Cálculo con el Iris**
Covarianza condicional pétalo | sépalo:
$\Sigma_{11} = \begin{bmatrix} 0.6857 & -0.0424 \\ -0.0424 & 0.1900 \end{bmatrix} \quad \text{← cov sépalos}$
$\Sigma_{22} = \begin{bmatrix} 3.1163 & 1.2956 \\ 1.2956 & 0.5810 \end{bmatrix} \quad \text{← cov pétalos}$
$\Sigma_{21} = \begin{bmatrix} 1.2743 & -0.3297 \\ 0.5163 & -0.1216 \end{bmatrix} \quad \text{← cov cruzada}$

$\det(\Sigma_{11}) = 0.6857(0.190) - (-0.0424)^2 = 0.1303 - 0.0018 = 0.1285$
$\Sigma_{11}^{-1} = \frac{1}{0.1285} \begin{bmatrix} 0.1900 & 0.0424 \\ 0.0424 & 0.6857 \end{bmatrix} = \begin{bmatrix} 1.479 & 0.330 \\ 0.330 & 5.336 \end{bmatrix}$

$\Sigma_{21} \Sigma_{11}^{-1} \approx \begin{bmatrix} 1.2743(1.479) + (-0.3297)(0.330) & \dots \\ \dots & \dots \end{bmatrix} = \begin{bmatrix} 1.775 & \dots \\ \dots & \dots \end{bmatrix}$

$\Sigma_{2|1} = \Sigma_{22} - \Sigma_{21} \Sigma_{11}^{-1} \Sigma_{12} \approx \begin{bmatrix} 3.1163 - 2.786 & 1.2956 - 1.157 \\ 1.2956 - 1.157 & 0.5810 - 0.477 \end{bmatrix} = \begin{bmatrix} 0.330 & 0.139 \\ 0.139 & 0.104 \end{bmatrix}$

Varianza pet.len sin condicionar: 3.116
Varianza pet.len dado el sépalo: 0.330 $\quad \text{← ¡reducción del 89\%!}$
> **🔑 Conclusión:** El complemento de Schur reduce la varianza del pétalo de 3.12 a 0.33 al condicionar sobre el sépalo: una reducción del 89%. El sépalo contiene información casi completa sobre el pétalo.

---

### Tema 39 | Derivadas Matriciales (Optimización sobre matrices)

**🌸 Dummies**
Las *derivadas matriciales* permiten optimizar funciones que dependen de matrices enteras. El gradiente de la pérdida respecto a los pesos nos dice cómo actualizarlos para clasificar mejor el Iris.

**∑ Algebraico**
Derivadas respecto a vector $x$:
$\frac{\partial(a^T x)}{\partial x} = a$
$\frac{\partial(x^T A x)}{\partial x} = (A+A^T)x = 2Ax \quad \text{(A simétrica)}$
$\frac{\partial\|Ax-b\|^2}{\partial x} = 2A^T(Ax-b)$

Derivadas respecto a matriz $X$:
$\frac{\partial\text{tr}(AX)}{\partial X} = A^T$
$\frac{\partial\text{tr}(X^T A X)}{\partial X} = (A+A^T)X = 2AX \quad \text{(A simétrica)}$
$\frac{\partial\log\det(X)}{\partial X} = X^{-T} = (X^T)^{-1}$

Regla de la cadena: $\frac{\partial f(g(x))}{\partial x} = \left(\frac{\partial g}{\partial x}\right)^T \cdot \frac{\partial f}{\partial g}$.

**🔢 Cálculo con el Iris**
Estimación MV de $\mu$ y $\Sigma$ — derivando la log-verosimilitud:
$\ell(\mu,\Sigma) = -\frac{n}{2}\log\det(\Sigma) - \frac{1}{2}\sum_i (x_i-\mu)^T \Sigma^{-1} (x_i-\mu)$

$\frac{\partial \ell}{\partial \mu} = \Sigma^{-1} \sum_i (x_i-\mu) = 0 \implies \hat{\mu} = \frac{1}{n}\sum_i x_i = \bar{x}$

$\frac{\partial \ell}{\partial \Sigma^{-1}} = \frac{n}{2}\Sigma - \frac{1}{2}\sum_i (x_i-\hat{\mu})(x_i-\hat{\mu})^T = 0 \implies \hat{\Sigma} = \frac{1}{n}\sum_i (x_i-\hat{\mu})(x_i-\hat{\mu})^T$

Las fórmulas que hemos usado todo el cuadernillo son exactamente los Estimadores de Máxima Verosimilitud.
Verificación numérica (1ª variable, Setosa):
$\hat{\mu}_{s[1]} = (5.1 + 4.9 + 4.7 + \dots) / 50 = 5.006$ ✓
$\hat{\Sigma}_{s[1,1]} = \text{Var}(\text{sep.len | Setosa}) = 0.1242$ ✓

---

### Tema 40 | Métrica de Riemann e Información de Fisher (Geometría curva)

**🌸 Dummies**
Una *métrica de Riemann* es un producto escalar que varía suavemente de punto en punto — la geometría puede ser distinta en cada lugar. En el espacio estadístico, la métrica natural es la *matriz de información de Fisher*.
Para el Iris: Setosa tiene pétalos muy concentrados, por lo que el espacio es más "curvo" allí — es más fácil distinguir dos Setosas que dos Virginicas con las mismas diferencias brutas.

**∑ Algebraico**
Métrica de Fisher:
$$g_{ij}(\theta) = \mathbb{E}\left[ \frac{\partial\log p}{\partial\theta_i} \cdot \frac{\partial\log p}{\partial\theta_j} \right] = I_{ij}(\theta)$$
Para gaussiana univariada $p(x;\mu,\sigma^2)$:
$$I(\mu,\sigma^2) = \begin{bmatrix} 1/\sigma^2 & 0 \\ 0 & 1/(2\sigma^4) \end{bmatrix}$$
Cramer-Rao: $\text{Var}(\hat{\theta}) \geq I(\theta)^{-1}$.

**🔢 Cálculo con el Iris**
Información de Fisher por especie (variable pet.len).
Varianzas intra-especie:
$\sigma^2(\text{Setosa, pet.len}) = 0.0302 \quad \text{← muy concentrada}$
$\sigma^2(\text{Versicolor, pet.len}) = 0.2211 \quad \text{← más dispersa}$
$\sigma^2(\text{Virginica, pet.len}) = 0.3049 \quad \text{← más dispersa aún}$

Información de Fisher $I_{11} = 1/\sigma^2$ para $\mu$:
$I(\text{Setosa}) = 1/0.0302 = 33.1 \quad \text{← altísima información}$
$I(\text{Versicolor}) = 1/0.2211 = 4.5$
$I(\text{Virginica}) = 1/0.3049 = 3.3 \quad \text{← poca información}$

Cota de Cramér-Rao ($n=50$ muestras):
$\text{Var}(\hat{\mu}_s) \geq 1/(50 \cdot 33.1) = 0.000604 \implies \sigma_{\text{est}} = 0.0246$
$\text{Var}(\hat{\mu}_{vi}) \geq 1/(50 \cdot 3.3) = 0.00606 \implies \sigma_{\text{est}} = 0.0778$
Estimamos $\mu_{\text{Setosa}}$ 3× más precisamente que $\mu_{\text{Virginica}}$ con las mismas muestras.

---

### Tema 41 | Cholesky y Raíz Cuadrada de Matrices (Factorizando la covarianza)

**🌸 Dummies**
La *descomposición de Cholesky* factoriza una matriz definida positiva como $\Sigma = LL^T$, donde $L$ es triangular inferior. Es como la raíz cuadrada matricial, y es más eficiente que calcular SVD. Para el Iris permite generar datos sintéticos de flores gaussianas.

**∑ Algebraico**
$A$ def. positiva $\iff \exists! L$ triangular inferior con diag $> 0 : A = LL^T$.
Fórmulas:
$L_{jj} = \sqrt{A_{jj} - \sum_{k<j} L_{jk}^2}$
$L_{ij} = \frac{1}{L_{jj}} \left( A_{ij} - \sum_{k<j} L_{ik}L_{jk} \right) \quad (i>j)$

Raíz cuadrada matricial: $\sqrt{\Sigma} = Q \sqrt{\Lambda} Q^T$.
Generación de datos gaussianos sintéticos: $x = \mu + L \cdot z, \ z \sim N(0,I) \implies x \sim N(\mu, \Sigma)$.

**🔢 Cálculo con el Iris**
Cholesky de $\Sigma_{\text{pooled}}$ (primeros 2 pasos):
$\Sigma_{\text{pooled}} = \begin{bmatrix} 0.265 & 0.093 & 0.168 & 0.038 \\ 0.093 & 0.115 & 0.055 & 0.033 \\ 0.168 & 0.055 & 0.186 & 0.042 \\ 0.038 & 0.033 & 0.042 & 0.043 \end{bmatrix}$

Columna 1:
$L_{11} = \sqrt{0.265} = 0.5148$
$L_{21} = 0.093 / 0.5148 = 0.1806$
$L_{31} = 0.168 / 0.5148 = 0.3263$
$L_{41} = 0.038 / 0.5148 = 0.0738$

Columna 2:
$L_{22} = \sqrt{0.115 - 0.1806^2} = \sqrt{0.115 - 0.0326} = \sqrt{0.0824} = 0.2871$
$L_{32} = (0.055 - 0.3263 \cdot 0.1806) / 0.2871 = (0.055 - 0.0589) / 0.2871 = -0.0136$
$L_{42} = (0.033 - 0.0738 \cdot 0.1806) / 0.2871 = (0.033 - 0.0133) / 0.2871 = 0.0686$

Resultado parcial $L$:
$$L \approx \begin{bmatrix} 0.5148 & 0 & 0 & 0 \\ 0.1806 & 0.2871 & 0 & 0 \\ 0.3263 & -0.0136 & \dots & 0 \\ 0.0738 & 0.0686 & \dots & \dots \end{bmatrix}$$

Verificación: $L_{11}^2 = 0.5148^2 = 0.265$ ✓, $L_{21} L_{11} = 0.1806 \cdot 0.5148 = 0.093$ ✓.

---

### Tema 42 | Normas Vectoriales y Matriciales (Midiendo tamaños en el espacio)

**🌸 Dummies**
La norma que eliges afecta qué consideras "grande" y qué "pequeño". Para el Iris, diferentes normas penalizan de forma diferente las desviaciones grandes de las pequeñas.

**∑ Algebraico**
Norma $p$ vectorial: $\|v\|_p = (\sum |v_i|^p)^{1/p}$.
$\|v\|_1 = \sum |v_i|$ (suma de absolutos)
$\|v\|_2 = \sqrt{\sum v_i^2}$ (euclídea)
$\|v\|_\infty = \max |v_i|$ (máximo)

Normas matriciales inducidas:
$\|A\|_2 = \sigma_{\max}(A)$ (espectral)
$\|A\|_F = \sqrt{\sum a_{ij}^2}$ (Frobenius)
$\|A\|_1 = \max_j \sum_i |a_{ij}|$ (máxima suma columna)

Desigualdades: $\|v\|_\infty \leq \|v\|_2 \leq \|v\|_1 \leq \sqrt{n}\|v\|_2 \leq n\|v\|_\infty$.

**🔢 Cálculo con el Iris**
Diferencia $d = \mu_{ve} - \mu_s = [0.930, -0.658, 2.798, 1.080]^T$.
$\|d\|_1 = |0.930| + |-0.658| + |2.798| + |1.080| = 5.466$
$\|d\|_2 = \sqrt{0.865 + 0.433 + 7.829 + 1.166} = \sqrt{10.293} = 3.208$
$\|d\|_\infty = \max(0.930, 0.658, 2.798, 1.080) = 2.798 \quad \text{← pétalo domina}$

Verificación: $2.798 \leq 3.208 \leq 5.466$ ✓.
Comparación matricial de $\Sigma_{\text{total}}$:
$\|\Sigma\|_2 = \sigma_{\max} = \lambda_{\max} = 4.228$
$\|\Sigma\|_F = 4.236$
$\|\Sigma\|_2 \leq \|\Sigma\|_F \leq \sqrt{4}\|\Sigma\|_2 = 8.456$ ✓.

---

### Tema 43 | Número de Condición (Sensibilidad numérica)

**🌸 Dummies**
Mide cuánto se amplifican los errores al resolver un sistema lineal. Una matriz mal condicionada es casi singular. Si la covarianza está mal condicionada, la inversa $\Sigma^{-1}$ y la distancia de Mahalanobis son numéricamente inestables.

**∑ Algebraico**
$$\kappa(A) = \|A\|_2 \|A^{-1}\|_2 = \frac{\sigma_{\max}}{\sigma_{\min}} = \frac{\lambda_{\max}}{\lambda_{\min}} \quad \text{(A simétrica def. pos.)}$$
$\kappa(A) \geq 1$. $\kappa(A)=1 \iff A = \alpha I$. $\kappa \gg 1 \to \text{mal condicionada}$.

**🔢 Cálculo con el Iris**
Números de condición:
$\Sigma_{\text{total}}$: $\lambda_{\max} = 4.2282, \lambda_{\min} = 0.0237 \implies \kappa(\Sigma_{\text{total}}) = 4.2282 / 0.0237 = 178.4$. Moderadamente condicionada.
$\Sigma_{\text{pooled}}$: $\lambda_{\max} \approx 0.360, \lambda_{\min} \approx 0.032 \implies \kappa(\Sigma_{\text{pooled}}) = 0.360 / 0.032 = 11.25$. Bien condicionada.
Identidad: $\kappa(I) = 1$. $\kappa(\Sigma_{\text{total}})$ es 178× peor que ideal.
Regularización $\Sigma_\lambda = \Sigma + \lambda I$:
$\kappa(\Sigma_{\text{total}} + 0.1I) = (4.228+0.1)/(0.024+0.1) = 4.328/0.124 = 34.9$ (baja de 178 a 35).

---

### Tema 44 | Teorema Rango-Nulidad Extendido (Cuatro subespacios)

**🌸 Dummies**
Toda matriz $A \in \mathbb{R}^{m \times n}$ tiene cuatro subespacios fundamentales: columna, fila, nulo, y nulo izquierdo. Descomponen $\mathbb{R}^n$ y $\mathbb{R}^m$ ortogonalmente.
Para la matriz de datos $X$: el espacio columna es lo que las flores "generan", el espacio nulo es lo que $X$ destruye.

**∑ Algebraico**
$\text{Col}(A) = \text{Im}(A) = \{Ax : x \in \mathbb{R}^n\} \subseteq \mathbb{R}^m, \dim=r$
$\text{Nul}(A) = \ker(A) = \{x : Ax=0\} \subseteq \mathbb{R}^n, \dim=n-r$
$\text{Col}(A^T) = \text{Im}(A^T) = \{A^T y : y \in \mathbb{R}^m\} \subseteq \mathbb{R}^n, \dim=r$
$\text{Nul}(A^T) = \ker(A^T) = \{y : A^T y=0\} \subseteq \mathbb{R}^m, \dim=m-r$

Ortogonalidad fundamental:
$\text{Col}(A) \perp \text{Nul}(A^T)$ y $\mathbb{R}^m = \text{Col}(A) \oplus \text{Nul}(A^T)$
$\text{Col}(A^T) \perp \text{Nul}(A)$ y $\mathbb{R}^n = \text{Col}(A^T) \oplus \text{Nul}(A)$

**🔢 Cálculo con el Iris**
4 subespacios de $X_c$ ($150 \times 4$, datos centrados). $\text{rang}(X_c) = 4 \implies r=4, m=150, n=4$.
$\text{Col}(X_c) \subseteq \mathbb{R}^{150}, \dim=4$ (Las 150 flores viven en un subespacio 4D de $\mathbb{R}^{150}$).
$\text{Nul}(X_c) \subseteq \mathbb{R}^4, \dim=4-4=0$ (Núcleo trivial: $X_c$ no aplana ninguna dirección de $\mathbb{R}^4$. Variables independientes).
$\text{Col}(X_c^T) \subseteq \mathbb{R}^4, \dim=4$ (= todo $\mathbb{R}^4$).
$\text{Nul}(X_c^T) \subseteq \mathbb{R}^{150}, \dim=150-4=146$ (Subespacio 146D ortogonal a las flores: patrones de pesos sin señal).

Verificación rango-nulidad:
$\dim\text{Col}(A) + \dim\text{Nul}(A) = 4 + 0 = 4 = n$ ✓
$\dim\text{Col}(A) + \dim\text{Nul}(A^T) = 4 + 146 = 150 = m$ ✓

---

## 📦 BLOQUE ∞: SÍNTESIS FINAL

### Tema 45 | El Iris como Objeto Matemático Completo

**∞ La imagen completa**
El dataset Iris de Fisher no es sólo 150 flores con 4 medidas. Es un objeto matemático completo que vive simultáneamente en múltiples estructuras algebraicas y geométricas. Todo lo que hemos construido en 45 temas converge aquí.

**Resumen por Bloques:**
* **Tema 1–5 (Álgebra Lineal):** $\mathbb{R}^4$, subespacios, bases. Las flores viven en $\dim=4$, las 3 medias generan un subespacio de $\dim=3$.
* **Tema 6–10 (Geometría):** $d(\mu_s,\mu_{ve})=3.21$, $\theta(\mu_{ve},\mu_{vi})=5.4^\circ$. Gram-Schmidt ortonormaliza las 3 medias.
* **Tema 11–15 (Matrices):** $\text{rang}(X)=4$, $\det(\Sigma_p)=2.4\times 10^{-5}$. Transformaciones que centran y proyectan.
* **Tema 16–19 (Eigenvalores):** $\lambda_1=4.228$ captura el 92.46%. Rotación ortogonal $Q$ del PCA.
* **Tema 20–23 (Formas):** Sylvester confirma $\Sigma$ def. positiva. $\|\Sigma\|_F=4.236$. Varianza total $\text{tr}(\Sigma)=4.573$.
* **Tema 24–26 (Análisis):** $\nabla\ell$ apunta $\mu_{ve} \to \mu_s$. $H(\text{Mahal})=2\Sigma^{-1}$. Jacobiano softmax cuantifica sensibilidad.
* **Tema 27–28 (Dual):** $\varphi_{pet}$ separa perfectamente: $1.71 / 5.59 / 7.58$ por especie. Aniquilador de $\dim=3$.
* **Tema 29–30 (Tensores):** $\Sigma$ tensor (0,2). $r_{34}=0.963$. Invariante bajo cambio de unidades.
* **Tema 31–44 (Aplicaciones):** PCA 92%, SVD $\sigma_1=25.1$, LDA $\lambda=32.2$, Mahal=7.71, Schur reduce var. 89%.

**🔢 La tabla maestra — todos los invariantes del Iris**

| Invariante | Valor | Tema | Significado |
| :--- | :--- | :--- | :--- |
| $\dim(\mathbb{R}^4)$ | 4 | 4 | 4 variables morfológicas independientes |
| $\text{rang}(X_c)$ | 4 | 13 | Sin relaciones lineales exactas |
| $\text{tr}(\Sigma_{\text{total}})$ | 4.573 | 23 | Varianza total del dataset |
| $\det(\Sigma_{\text{pooled}})$ | $2.41\times 10^{-5}$ | 15 | Volumen elipsoide intra-especie |
| $\lambda_1(\Sigma_{\text{total}})$ | 4.228 | 16 | Varianza del PC1 |
| $\text{VE}(\text{PC1})$ | 92.46% | 31 | 1 dimensión captura casi todo |
| $\text{VE}(\text{PC1}+\text{PC2})$ | 97.77% | 31 | 2D prácticamente completo |
| $\theta(\mu_{ve}, \mu_{vi})$ | 5.4° | 8 | Ve y Vi casi misma dirección |
| $d_E(\mu_s,\mu_{ve})$ | 3.208 | 7 | Distancia euclídea Setosa-Versicolor |
| $d_M(\mu_s,\mu_{ve})$ | 7.712 | 32 | Distancia de Mahalanobis |
| $\sigma_1(X_c)$ | 25.10 | 33 | Primer valor singular (SVD) |
| $\lambda_{\text{LD1}}(\text{LDA})$ | 32.19 | 34 | Potencia discriminante eje 1 |
| $r(\text{pet.len,pet.wid})$ | 0.963 | 29 | Correlación pétalo-pétalo |
| $\kappa(\Sigma_{\text{total}})$ | 178.4 | 43 | Número de condición |
| $\text{Var}(\text{pet|sep})$ | 0.330 | 38 | Var. condicional (Schur): -89% |

> **∞ La lección profunda:** El dataset Iris es una **variedad estadística de dimensión efectiva 1**, incrustada en $\mathbb{R}^4$. Toda su riqueza se puede comprender con un solo eigenvector (PC1 = tamaño del pétalo), que explica el 92% de la varianza y separa perfectamente las tres especies. Las 45 estructuras algebraicas no son herramientas separadas: son **45 formas de ver el mismo objeto desde ángulos distintos**. El Iris es el prisma; el álgebra es la luz.

**Diagrama de dependencias — todo converge:**
```text
Espacio Vectorial (1)
    ↓
Base + Dimensión (4)  →  Cambio de Base (14)  →  Diagonalización (17)
    ↓                                              ↓
Producto Escalar (6)  →  Gram-Schmidt (10)      →  PCA (31)
    ↓                                              ↓
Norma + Distancia (7)  →  Mahalanobis (32)  ←  Sylvester (22)
    ↓                           ↓
Eigenvalores (16)  →  SVD (33)  →  LDA (34)  →  Hiperplanos (35)
    ↓
Formas Cuadráticas (21)  →  Hessiano (26)  →  Deriv. Matriciales (39)
    ↓
Dual (27)  →  Tensores (29)  →  Schur (38)  →  Riemann (40)
