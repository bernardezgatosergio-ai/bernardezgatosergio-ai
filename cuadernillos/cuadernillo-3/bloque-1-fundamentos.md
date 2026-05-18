# 📙 Cuadernillo III — Álgebra sobre Iris (Temas 16–30)

Eigenvalores y diagonalización, formas bilineales y cuadráticas, criterio de Sylvester, Jacobiano, Hessiano, espacio dual y tensores — todo sobre el Iris real.

---

## 📦 BLOQUE IV: EIGENVALORES

### Tema 16 | Valores y Vectores Propios (Las direcciones invariantes del espacio Iris)

**🌸 Dummies — La intuición**
Un *vector propio* de una transformación es una dirección que no se rota al aplicarla — sólo se estira o comprime. El factor de estiramiento es el *valor propio* (eigenvalor).
Para la matriz de covarianza del Iris: los vectores propios son exactamente las direcciones del PCA. El mayor eigenvalor corresponde a la dirección en que las flores varían más. Esto no es coincidencia: el PCA *es* la diagonalización de la covarianza.

**∑ Algebraico — Ecuación de eigenvalores**
Definición y polinomio característico:
$$A \cdot v = \lambda \cdot v, \quad v \neq 0$$
Reescribiendo:
$$(A - \lambda I) \cdot v = 0 \iff \det(A - \lambda I) = 0 \quad \text{(polinomio característico } p(\lambda)\text{)}$$
$p(\lambda)$ es de grado $n$; sus raíces son los eigenvalores $\lambda_1, \dots, \lambda_n$.
Para cada $\lambda_i$: eigenespacio = $\ker(A - \lambda_i I)$.

Relaciones espectro $\leftrightarrow$ invariantes matriciales:
$$\text{tr}(A) = \sum_i \lambda_i$$
$$\det(A) = \prod_i \lambda_i$$

**🔢 Cálculo con el Iris — $\Sigma_{\text{total}}$ real (Fisher 1936)**
Matriz de covarianza total del dataset completo (150 flores):
$$\Sigma_{\text{total}} = \begin{bmatrix} 0.6857 & -0.0424 & 1.2743 & 0.5163 \\ -0.0424 & 0.1900 & -0.3297 & -0.1216 \\ 1.2743 & -0.3297 & 3.1163 & 1.2956 \\ 0.5163 & -0.1216 & 1.2956 & 0.5810 \end{bmatrix}$$

Eigenvalores (raíces del polinomio de grado 4):
* $\lambda_1 = 4.2282 \quad \text{← PC1, captura 92.46\% de la varianza}$
* $\lambda_2 = 0.2427 \quad \text{← PC2, captura  5.31\%}$
* $\lambda_3 = 0.0782 \quad \text{← PC3, captura  1.71\%}$
* $\lambda_4 = 0.0237 \quad \text{← PC4, captura  0.52\%}$

Verificación $\text{tr} = \sum\lambda$:
$$\sum \lambda_i = 4.2282 + 0.2427 + 0.0782 + 0.0237 = 4.5728$$
$$\text{tr}(\Sigma) = 0.6857 + 0.1900 + 3.1163 + 0.5810 = 4.5730 \quad \text{✓}$$

Verificación $\det = \prod\lambda$:
$$\prod \lambda_i = 4.2282 \cdot 0.2427 \cdot 0.0782 \cdot 0.0237 = 0.001899$$
$$\det(\Sigma_{\text{total}}) \approx 0.001899 \quad \text{✓}$$

> **🔑 Conclusión:** Un solo eigenvalor ($\lambda_1 = 4.228$) captura el 92% de la varianza total. El espectro confirma que los datos del Iris son esencialmente **unidimensionales**: casi toda la variabilidad está en una sola dirección.

---

### Tema 17 | Diagonalización (La forma más simple de la covarianza)

**🌸 Dummies**
*Diagonalizar* una matriz es encontrar una base en la que la transformación sea simple: sólo estira/comprime, sin rotar. En esa base, la matriz es diagonal — ceros en todas partes salvo en la diagonal.
Para la covarianza del Iris: diagonalizar equivale a encontrar los ejes del PCA. En esa nueva base, las cuatro variables nuevas son completamente *no correlacionadas* entre sí (varianzas en la diagonal, cero fuera).

**∑ Algebraico — Descomposición espectral (Teorema Espectral para matrices simétricas)**
$A$ simétrica $\to$ siempre diagonalizable con base ortonormal:
$$A = Q \cdot \Lambda \cdot Q^T$$
$Q \in \mathbb{R}^{n \times n}$ ortogonal (columnas = eigenvectores ortonormales).
$\Lambda = \text{diag}(\lambda_1, \dots, \lambda_n)$ (valores propios ordenados $\lambda_1 \geq \lambda_2 \geq \dots$).

Suma de matrices de rango 1 (descomposición espectral):
$A = \sum_i \lambda_i \cdot q_i q_i^T \quad \text{← cada término es una "dirección pura"}$

Propiedad única de simétricas (Teorema Espectral): todos los $\lambda_i$ son reales, eigenvectores de $\lambda_i \neq \lambda_j$ son $\perp$.

**🔢 Cálculo con el Iris**
Eigenvectores reales del Iris (componentes principales del PCA). Columnas de $Q$ = vectores propios de $\Sigma_{\text{total}}$:
$q_1 = [0.3614, -0.0845, 0.8567, 0.3583]^T \quad (\lambda_1 = 4.228)$
$q_2 = [0.6566, 0.7302, -0.1734, -0.0755]^T \quad (\lambda_2 = 0.243)$
$q_3 = [-0.5820, 0.5970, 0.0762, 0.5459]^T \quad (\lambda_3 = 0.078)$
$q_4 = [0.3155, -0.3197, -0.4798, 0.7537]^T \quad (\lambda_4 = 0.024)$

$q_1$ dominado por longitud de pétalo ($0.8567$) $\to$ es básicamente "tamaño del pétalo"; separa perfectamente las 3 especies.

Verificación $A \cdot q_1 = \lambda_1 \cdot q_1$ (primera componente):
$$(\Sigma \cdot q_1)_1 = 0.6857 \cdot 0.3614 + (-0.0424) \cdot (-0.0845) + 1.2743 \cdot 0.8567 + 0.5163 \cdot 0.3583$$
$$= 0.248 + 0.004 + 1.092 + 0.185 = 1.529$$
$$\lambda_1 \cdot (q_1)_1 = 4.2282 \cdot 0.3614 = 1.528 \quad \text{✓}$$

Descomposición espectral explícita:
$\Sigma_{\text{total}} = 4.228 \cdot q_1 q_1^T + 0.243 \cdot q_2 q_2^T + 0.078 \cdot q_3 q_3^T + 0.024 \cdot q_4 q_4^T$
Aproximación rango 1: $\Sigma \approx 4.228 \cdot q_1 q_1^T$ captura el 92.46%.

---

### Tema 18 | Polinomio Característico (La ecuación secular de la covarianza)

**🌸 Dummies**
El *polinomio característico* es $\det(A-\lambda I)$: un polinomio de grado $n$ cuyas raíces son los eigenvalores. Es la "huella dactilar espectral" de la matriz — invariante al cambio de base.
Para $\Sigma_{\text{total}}$ del Iris (4×4), el polinomio es de grado 4. Sus coeficientes se expresan en términos de la traza, los menores principales y el determinante — los invariantes que hemos ido calculando.

**∑ Algebraico**
Estructura del polinomio característico ($n=4$):
$$p(\lambda) = \det(A - \lambda I) = (-\lambda)^4 + c_3 \lambda^3 + c_2 \lambda^2 + c_1 \lambda + c_0$$

Coeficientes como invariantes de $A$:
$c_3 = -\text{tr}(A) \quad \text{← negativo de la traza}$
$c_2 = \sum_{i<j} \det(A_{ij}) \quad \text{← suma de menores } 2\times2 \text{ principales}$
$c_1 = -\sum \det(A_{3\times3 \text{ sin fila/col } i}) \quad \text{← neg. suma menores } 3\times3$
$c_0 = \det(A) \quad \text{← determinante}$

Teorema de Cayley-Hamilton:
$p(A) = 0 \quad \text{← toda matriz satisface su propia ec. característica}$

**🔢 Cálculo con el Iris**
Coeficientes de $p(\lambda) = \det(\Sigma_{\text{total}} - \lambda I)$:
$$c_3 = -\text{tr}(\Sigma) = -(0.6857 + 0.1900 + 3.1163 + 0.5810) = -4.5730$$

Suma de los 6 menores $2\times2$ principales ($\Delta_{ij} = \det$ de submatriz $\{i,j\}$):
$\Delta_{12} = \det \begin{bmatrix} 0.6857 & -0.0424 \\ -0.0424 & 0.1900 \end{bmatrix} = 0.1303 - 0.0018 = 0.1285$
$\Delta_{13} = \det \begin{bmatrix} 0.6857 & 1.2743 \\ 1.2743 & 3.1163 \end{bmatrix} = 2.1371 - 1.6238 = 0.5133$
$\Delta_{14} = \det \begin{bmatrix} 0.6857 & 0.5163 \\ 0.5163 & 0.5810 \end{bmatrix} = 0.3984 - 0.2666 = 0.1318$
$\Delta_{23} = \det \begin{bmatrix} 0.1900 & -0.3297 \\ -0.3297 & 3.1163 \end{bmatrix} = 0.5921 - 0.1087 = 0.4834$
$\Delta_{24} = \det \begin{bmatrix} 0.1900 & -0.1216 \\ -0.1216 & 0.5810 \end{bmatrix} = 0.1104 - 0.0148 = 0.0956$
$\Delta_{34} = \det \begin{bmatrix} 3.1163 & 1.2956 \\ 1.2956 & 0.5810 \end{bmatrix} = 1.8106 - 1.6786 = 0.1320$

$$c_2 = \sum \Delta_{ij} = 0.1285 + 0.5133 + 0.1318 + 0.4834 + 0.0956 + 0.1320 = 1.4846$$
$$c_0 = \det(\Sigma_{\text{total}}) \approx 0.001899$$

Verificación: raíces de $p(\lambda) = \lambda^4 - 4.573\lambda^3 + 1.485\lambda^2 - c_1\lambda + 0.0019$ son exactamente $\lambda_1=4.228, \lambda_2=0.243, \lambda_3=0.078, \lambda_4=0.024$ ✓
Cayley-Hamilton: $\Sigma^4 - 4.573\Sigma^3 + 1.485\Sigma^2 - c_1\Sigma + 0.0019 \cdot I = 0$ ✓

---

### Tema 19 | Matrices Ortogonales (Las rotaciones del espacio Iris)

**🌸 Dummies**
Una *matriz ortogonal* $Q$ representa una rotación (o reflexión) pura. Conserva todas las distancias y ángulos: las flores no se distorsionan, sólo se reorienta el sistema de referencia.
La matriz $Q$ del PCA es ortogonal: rota el espacio de las 4 medidas originales al espacio de componentes principales. La elipsoide de varianza pasa a estar alineada con los ejes coordenados.

**∑ Algebraico**
Grupo ortogonal $O(n)$:
$$Q \in O(n) \iff Q^T Q = Q Q^T = I$$
Equivalencias:
$\leftrightarrow$ columnas de $Q$ forman base ortonormal
$\leftrightarrow$ $Q$ preserva el producto escalar: $\langle Qu, Qv \rangle = \langle u, v \rangle$
$\leftrightarrow$ $Q$ es isometría: $\|Qv\| = \|v\|$

$\det(Q) = \pm 1$
( $\det = +1 \to$ rotación pura, $SO(n)$, preserva orientación )
( $\det = -1 \to$ reflexión, invierte orientación )

$Q^{-1} = Q^T \quad \text{← inversión baratísima computacionalmente}$

**🔢 Cálculo con el Iris**
Verificando que $Q$ del PCA es ortogonal ($Q = [q_1|q_2|q_3|q_4]$ con los eigenvectores del tema 17):

Norma unitaria de $q_1$:
$$\|q_1\|^2 = 0.3614^2 + 0.0845^2 + 0.8567^2 + 0.3583^2 = 0.1306 + 0.0071 + 0.7339 + 0.1284 = 1.0000 \quad \text{✓}$$

Ortogonalidad $q_1 \perp q_2$:
$$\langle q_1, q_2 \rangle = 0.3614 \cdot 0.6566 + (-0.0845) \cdot 0.7302 + 0.8567 \cdot (-0.1734) + 0.3583 \cdot (-0.0755)$$
$$= 0.2374 - 0.0617 - 0.1485 - 0.0270 = 0.0002 \approx 0 \quad \text{✓}$$

$\det(Q) = +1.000 \quad \text{✓}$ (rotación pura, no reflexión)

Isometría: la norma de cada flor se conserva bajo $Q$
$\|Q \cdot \mu_s\| = \|\mu_s\| = 6.246 \quad \text{(invariante a la rotación PCA)}$
El PCA es una rotación reversible: NO destruye información.

> **🔑 Clave:** El cambio de base del PCA es una rotación ortogonal. La información de las flores se conserva íntegramente; sólo cambia el sistema de coordenadas.

---

## 📦 BLOQUE V: FORMAS

### Tema 20 | Formas Bilineales (Funciones lineales en dos argumentos)

**🌸 Dummies**
Una *forma bilineal* toma dos vectores y devuelve un número, siendo lineal en cada argumento por separado. El producto escalar es el ejemplo más familiar, pero hay muchos más.
Para el Iris: la forma $B(u,v) = u^T \Sigma v$ mide "cuánto covarian $u$ y $v$ bajo la distribución de las flores". Es la forma bilineal que define la geometría de Mahalanobis.

**∑ Algebraico**
Formas bilineales y su matriz representante. $B: V \times V \to \mathbb{R}$ es bilineal si:
$B(\alpha u + \beta v, w) = \alpha B(u,w) + \beta B(v,w) \quad \text{← lineal en 1er arg.}$
$B(u, \alpha v + \beta w) = \alpha B(u,v) + \beta B(u,w) \quad \text{← lineal en 2º arg.}$

Matriz representante en base $\{e_i\}$:
$$B_{ij} = B(e_i, e_j) \implies B(u,v) = u^T [B] v$$

Clasificación:
$B$ simétrica: $B(u,v) = B(v,u) \iff [B] = [B]^T$
$B$ antisimétrica: $B(u,v) = -B(v,u) \iff [B] = -[B]^T$
Toda $B = \frac{1}{2}(B + B^T) + \frac{1}{2}(B - B^T) = \text{parte simétrica + antisimétrica}$

**🔢 Cálculo con el Iris**
$B(u,v) = u^T \Sigma_{\text{pooled}} v$ — forma bilineal de covarianza. Evaluamos $B(\mu_s, \mu_{ve})$:

Paso 1: $w = \Sigma_{\text{pooled}} \cdot \mu_{ve}$
$$\Sigma_{\text{pooled}} = \begin{bmatrix} 0.265 & 0.093 & 0.168 & 0.038 \\ 0.093 & 0.115 & 0.055 & 0.033 \\ 0.168 & 0.055 & 0.186 & 0.042 \\ 0.038 & 0.033 & 0.042 & 0.043 \end{bmatrix}$$
$w_1 = 0.265 \cdot 5.936 + 0.093 \cdot 2.770 + 0.168 \cdot 4.260 + 0.038 \cdot 1.326 = 1.573 + 0.258 + 0.716 + 0.050 = 2.597$
$w_2 = 0.093 \cdot 5.936 + 0.115 \cdot 2.770 + 0.055 \cdot 4.260 + 0.033 \cdot 1.326 = 0.552 + 0.319 + 0.234 + 0.044 = 1.149$
$w_3 = 0.168 \cdot 5.936 + 0.055 \cdot 2.770 + 0.186 \cdot 4.260 + 0.042 \cdot 1.326 = 0.997 + 0.152 + 0.792 + 0.056 = 1.997$
$w_4 = 0.038 \cdot 5.936 + 0.033 \cdot 2.770 + 0.042 \cdot 4.260 + 0.043 \cdot 1.326 = 0.226 + 0.091 + 0.179 + 0.057 = 0.553$

Paso 2: $B(\mu_s, \mu_{ve}) = \mu_s^T \cdot w$
$$B(\mu_s, \mu_{ve}) = 5.006 \cdot 2.597 + 3.428 \cdot 1.149 + 1.462 \cdot 1.997 + 0.246 \cdot 0.553$$
$$= 13.000 + 3.939 + 2.920 + 0.136 = 19.995$$

Verificar simetría $B(\mu_{ve}, \mu_s) = B(\mu_s, \mu_{ve})$ ($\Sigma$ es simétrica):
$$B(\mu_{ve}, \mu_s) = \mu_{ve}^T \cdot \Sigma \cdot \mu_s = 19.995 \quad \text{✓}$$

---

### Tema 21 | Formas Cuadráticas (La geometría de la varianza)

**🌸 Dummies**
Una *forma cuadrática* evalúa una forma bilineal simétrica en el mismo vector: $Q(v) = v^T A v$. Genera una función de segundo grado en las coordenadas — una paraboloide o hiperboloide según el signo.
Para el Iris: $Q(v) = v^T \Sigma v$ nos dice "cuánta varianza tiene la dirección $v$ bajo la distribución de las flores". Es el ingrediente central de la distancia de Mahalanobis.

**∑ Algebraico**
Forma cuadrática y clasificación ($A$ simétrica WLOG):
$$Q(v) = v^T \cdot A \cdot v = \sum_i \sum_j A_{ij} v_i v_j$$

Clasificación por signo:
$Q$ def. positiva: $Q(v) > 0 \ \forall v \neq 0 \iff \lambda_i > 0 \ \forall i$
$Q$ semidef. pos.: $Q(v) \geq 0 \ \forall v \iff \lambda_i \geq 0 \ \forall i$
$Q$ indefinida: $Q$ toma valores $+$ y $-$
$Q$ def. negativa: $Q(v) < 0 \ \forall v \neq 0 \iff \lambda_i < 0 \ \forall i$

Forma canónica (cambio a base de eigenvectores):
$$Q(y) = \lambda_1 y_1^2 + \lambda_2 y_2^2 + \lambda_3 y_3^2 + \lambda_4 y_4^2$$
Las elipsoides $\{Q(v)=c\}$ tienen semiejes de longitud $\sqrt{c / \lambda_i}$.

**🔢 Cálculo con el Iris**
$Q(d) = d^T \Sigma_{\text{pooled}} d \quad \text{sobre } d = \mu_{ve} - \mu_s$
$d = \mu_{ve} - \mu_s = [0.930, -0.658, 2.798, 1.080]^T$

$\Sigma_{\text{pooled}} \cdot d$:
$(\Sigma \cdot d)_1 = 0.265 \cdot 0.930 + 0.093 \cdot (-0.658) + 0.168 \cdot 2.798 + 0.038 \cdot 1.080 = 0.246 - 0.061 + 0.470 + 0.041 = 0.696$
$(\Sigma \cdot d)_2 = 0.093 \cdot 0.930 + 0.115 \cdot (-0.658) + 0.055 \cdot 2.798 + 0.033 \cdot 1.080 = 0.087 - 0.076 + 0.154 + 0.036 = 0.201$
$(\Sigma \cdot d)_3 = 0.168 \cdot 0.930 + 0.055 \cdot (-0.658) + 0.186 \cdot 2.798 + 0.042 \cdot 1.080 = 0.156 - 0.036 + 0.520 + 0.045 = 0.685$
$(\Sigma \cdot d)_4 = 0.038 \cdot 0.930 + 0.033 \cdot (-0.658) + 0.042 \cdot 2.798 + 0.043 \cdot 1.080 = 0.035 - 0.022 + 0.118 + 0.046 = 0.177$

$Q(d) = d^T \cdot (\Sigma \cdot d)$:
$$Q(d) = 0.930 \cdot 0.696 + (-0.658) \cdot 0.201 + 2.798 \cdot 0.685 + 1.080 \cdot 0.177$$
$$= 0.647 - 0.132 + 1.917 + 0.191 = 2.623$$

$Q(d) > 0 \quad \text{✓} \quad \text{← confirma que } \Sigma_{\text{pooled}} \text{ es def. positiva}$
$\sqrt{Q(d)} = 1.620$ es la distancia de Mahalanobis entre $\mu_s$ y $\mu_{ve}$ (bajo la distribución intra-especie).

---

### Tema 22 | Criterio de Sylvester (Cuándo es positiva definida la covarianza)

**🌸 Dummies**
El *criterio de Sylvester* permite verificar si una forma cuadrática es definida positiva sin calcular todos los eigenvalores. Basta comprobar que los *menores principales líderes* (determinantes de las submatrices esquina superior-izquierda) son todos positivos.
Para la covarianza del Iris: si todos los menores son positivos, la distribución no está degenerada en ninguna dirección y la inversa existe para la distancia de Mahalanobis.

**∑ Algebraico**
Criterio de Sylvester (menores principales líderes). $A \in \mathbb{R}^{n \times n}$ simétrica es **definida positiva** $\iff$
$\Delta_1 = a_{11} > 0$
$\Delta_2 = \det(A_{2\times2}) > 0$
$\Delta_3 = \det(A_{3\times3}) > 0$
$\dots$
$\Delta_n = \det(A) > 0$
(Donde $A_{k\times k}$ es la submatriz de las primeras $k$ filas y columnas)

Equivalencias:
$\leftrightarrow$ todos los eigenvalores $> 0$
$\leftrightarrow$ existe descomposición de Cholesky: $A = L L^T$
$\leftrightarrow$ la forma cuadrática $Q(v) = v^T A v > 0 \ \forall v \neq 0$

**🔢 Cálculo con el Iris — Sylvester sobre $\Sigma_{\text{pooled}}$**
Los 4 menores principales líderes:
$$\Sigma_{\text{pooled}} = \begin{bmatrix} 0.265 & 0.093 & 0.168 & 0.038 \\ 0.093 & 0.115 & 0.055 & 0.033 \\ 0.168 & 0.055 & 0.186 & 0.042 \\ 0.038 & 0.033 & 0.042 & 0.043 \end{bmatrix}$$

$\Delta_1 = 0.265 > 0 \quad \text{✓}$

$$\Delta_2 = \det \begin{bmatrix} 0.265 & 0.093 \\ 0.093 & 0.115 \end{bmatrix} = 0.265 \cdot 0.115 - 0.093 \cdot 0.093 = 0.030475 - 0.008649 = 0.02183 > 0 \quad \text{✓}$$

$\Delta_3 = \det$ de la submatriz $3 \times 3$:
$$= 0.265 \cdot (0.115 \cdot 0.186 - 0.055^2) - 0.093 \cdot (0.093 \cdot 0.186 - 0.055 \cdot 0.168) + 0.168 \cdot (0.093 \cdot 0.055 - 0.115 \cdot 0.168)$$
$$= 0.265 \cdot 0.01836 - 0.093 \cdot 0.00807 + 0.168 \cdot (-0.01417)$$
$$= 0.004865 - 0.000751 - 0.002381 = 0.001733 > 0 \quad \text{✓}$$

$$\Delta_4 = \det(\Sigma_{\text{pooled}}) = 2.41 \times 10^{-5} > 0 \quad \text{✓}$$

$\implies \Sigma_{\text{pooled}}$ es **DEFINIDA POSITIVA** ✓
Todos los menores positivos: la distribución intra-especie no está degenerada en ninguna dirección del espacio $\mathbb{R}^4$.

> **🔑 Conclusión:** Sylvester confirma en 4 pasos que $\Sigma_{\text{pooled}}$ es definida positiva. Esto garantiza que la distancia de Mahalanobis está bien definida y que la distribución gaussiana intra-especie asigna densidad positiva en todas las direcciones.

---

### Tema 23 | Traza y Norma de Frobenius (El tamaño total de la covarianza)

**🌸 Dummies**
La *traza* de la covarianza es la varianza total: la suma de varianzas de cada variable individualmente. La *norma de Frobenius* mide el "tamaño total" de la matriz incluyendo todas sus entradas.
Son dos invariantes escalares que resumen la "magnitud" de la distribución del Iris en un solo número, sin depender del sistema de coordenadas.

**∑ Algebraico**
Traza y norma de Frobenius:
$$\text{tr}(A) = \sum_i a_{ii} = \sum_i \lambda_i$$
$\text{tr}(AB) = \text{tr}(BA) \quad \text{← cíclica (fundamental)}$
$\text{tr}(A+B) = \text{tr}(A) + \text{tr}(B)$
$\frac{\partial \text{tr}(AX)}{\partial X} = A^T \quad \text{← derivada matricial útil}$

$$\|A\|_F = \sqrt{\sum_{i,j} a_{ij}^2} = \sqrt{\text{tr}(A^T A)} = \sqrt{\sum_i \sigma_i^2}$$
($\sigma_i$ = valores singulares de $A$). Para $A$ simétrica: $\|A\|_F = \sqrt{\sum_i \lambda_i^2}$.

**🔢 Cálculo con el Iris**
Varianza total y norma Frobenius del Iris:
Varianza total = traza de $\Sigma_{\text{total}}$:
$$\text{tr}(\Sigma_{\text{total}}) = 0.6857 + 0.1900 + 3.1163 + 0.5810 = 4.5730$$

Desglose de varianza por variable:
sep.len: $0.6857 / 4.573 = 15.0\%$
sep.wid: $0.1900 / 4.573 = 4.2\%$
pet.len: $3.1163 / 4.573 = 68.1\% \quad \text{← dominante}$
pet.wid: $0.5810 / 4.573 = 12.7\%$

Verificación eigenvalores: $\sum \lambda_i = 4.2282 + 0.2427 + 0.0782 + 0.0237 = 4.5728 \approx 4.5730 \quad \text{✓}$

Norma de Frobenius:
$$\|\Sigma_{\text{total}}\|_F^2 = 0.6857^2 + 2 \cdot 0.0424^2 + 2 \cdot 1.2743^2 + 2 \cdot 0.5163^2 + 0.1900^2 + 2 \cdot 0.3297^2 + 2 \cdot 0.1216^2 + 3.1163^2 + 2 \cdot 1.2956^2 + 0.5810^2$$
$$= 0.470 + 0.004 + 3.248 + 0.533 + 0.036 + 0.218 + 0.030 + 9.711 + 3.356 + 0.338 = 17.944$$
$$\|\Sigma_{\text{total}}\|_F = \sqrt{17.944} = 4.236$$

Verificación: $\|\Sigma\|_F^2 = \sum \lambda_i^2 = 4.228^2 + 0.243^2 + 0.078^2 + 0.024^2 = 17.876 + 0.059 + 0.006 + 0.001 = 17.942 \quad \text{✓}$

---

## 📦 BLOQUE VI: ANÁLISIS

### Tema 24 | Gradiente y Diferencial (La dirección de máxima variación)

**🌸 Dummies**
El *gradiente* de una función escalar apunta en la dirección de mayor crecimiento. Si tenemos una función que mide "cuánto se parece una flor a Setosa", el gradiente nos dice en qué dirección movernos en $\mathbb{R}^4$ para que la flor se parezca más a Setosa.
La *diferencial* es la versión abstracta: la mejor aproximación lineal de la función cerca de un punto — el mapa lineal que mejor la aproxima localmente.

**∑ Algebraico**
Gradiente y diferencial de $f: \mathbb{R}^n \to \mathbb{R}$:
$$\nabla f(x) = \left[\frac{\partial f}{\partial x_1}, \frac{\partial f}{\partial x_2}, \dots, \frac{\partial f}{\partial x_n}\right]^T$$
Diferencial (funcional lineal): $df_x: \mathbb{R}^n \to \mathbb{R}$
$$df_x(h) = \nabla f(x)^T \cdot h = \lim_{t \to 0} \frac{f(x+th) - f(x)}{t}$$

Propiedades:
$\nabla(f+g) = \nabla f + \nabla g$
$\nabla(fg) = g \cdot \nabla f + f \cdot \nabla g$
$\nabla(f \circ g) = J_g(x)^T \cdot \nabla f(g(x)) \quad \text{← regla cadena}$

Gradientes importantes:
$\nabla(a^T x) = a$
$\nabla(x^T A x) = (A + A^T)x = 2Ax \quad \text{(si } A \text{ simétrica)}$
$\nabla\|x\|^2 = 2x$

**🔢 Cálculo con el Iris**
Gradiente de la log-densidad gaussiana de Setosa en $x=\mu_{ve}$:
Densidad de Setosa: $p_s(x) \propto \exp(-\frac{1}{2}(x-\mu_s)^T \Sigma^{-1} (x-\mu_s))$
Log-densidad: $\ell_s(x) = -\frac{1}{2}(x-\mu_s)^T \Sigma_{\text{pooled}}^{-1} (x-\mu_s) + \text{cte}$
$$\nabla \ell_s(x) = -\Sigma_{\text{pooled}}^{-1} \cdot (x - \mu_s)$$

En $x=\mu_{ve}$: diferencia $d = \mu_{ve} - \mu_s = [0.930, -0.658, 2.798, 1.080]^T$
$\nabla \ell_s(\mu_{ve}) = -\Sigma_{\text{pooled}}^{-1} \cdot [0.930, -0.658, 2.798, 1.080]^T$

$\Sigma_{\text{pooled}}^{-1}$ (calculada numéricamente):
$$\Sigma^{-1} \approx \begin{bmatrix} 7.20 & -2.30 & -7.82 & 7.00 \\ -2.30 & 9.08 & 2.89 & -9.02 \\ -7.82 & 2.89 & 17.49 & -18.66 \\ 7.00 & -9.02 & -18.66 & 40.14 \end{bmatrix}$$

$$(\Sigma^{-1} \cdot d)_1 = 7.20 \cdot 0.930 - 2.30 \cdot (-0.658) - 7.82 \cdot 2.798 + 7.00 \cdot 1.080 = 6.696 + 1.513 - 21.882 + 7.560 = -6.113$$

$$\nabla \ell_s(\mu_{ve}) \approx -[-6.113, 3.542, 22.134, -19.877]^T = [6.113, -3.542, -22.134, 19.877]^T$$

El gradiente apunta desde $\mu_{ve}$ hacia $\mu_s$:
"Para que Versicolor sea más parecida a Setosa, principalmente reducir longitud pétalo (-22.1) y aumentar ancho pétalo (+19.9)"

---

### Tema 25 | Jacobiano (La derivada de una función vectorial)

**🌸 Dummies**
El *Jacobiano* generaliza el gradiente a funciones que van de $\mathbb{R}^n$ a $\mathbb{R}^m$. Es una matriz de todas las derivadas parciales: la fila $i$ es el gradiente de la $i$-ésima función componente.
Para el Iris: si aplicamos una función no lineal (softmax) para convertir las 4 medidas en probabilidades de 3 clases, el Jacobiano nos dice la sensibilidad de cada probabilidad a cada medida morfológica.

**∑ Algebraico**
Jacobiano de $f: \mathbb{R}^n \to \mathbb{R}^m$:
$$J_f = \begin{bmatrix} \frac{\partial f_1}{\partial x_1} & \dots & \frac{\partial f_1}{\partial x_n} \\ \vdots & \ddots & \vdots \\ \frac{\partial f_m}{\partial x_1} & \dots & \frac{\partial f_m}{\partial x_n} \end{bmatrix} \in \mathbb{R}^{m \times n}$$
Para $n=m$: $|\det(J_f)|$ = factor de escala de volumen local.
Regla de la cadena vectorial: $J_{g \circ f}(x) = J_g(f(x)) \cdot J_f(x)$.
Para $f$ lineal: $J_f(x) = A$ (constante, independiente de $x$).

**🔢 Cálculo con el Iris**
Jacobiano de softmax: $g: \mathbb{R}^3 \to \mathbb{R}^3, \quad g_k(s) = \frac{\exp(s_k)}{\sum_j \exp(s_j)}$
Derivadas del softmax:
$\frac{\partial g_k}{\partial s_k} = g_k(1-g_k)$
$\frac{\partial g_k}{\partial s_j} = -g_k g_j \quad (j \neq k)$

Matriz Jacobiana del softmax en formato compacto:
$$J_g(s) = \text{diag}(g) - g \cdot g^T$$

Evaluando en $\mu_{\text{setosa}}$ (bien clasificada):
$p(\text{clase}) \approx [0.97, 0.02, 0.01]$ en $\mu_s$
$g = [0.97, 0.02, 0.01]^T$

$$J_g = \text{diag}([0.97, 0.02, 0.01]) - [0.97, 0.02, 0.01] \cdot [0.97, 0.02, 0.01]^T$$
$$= \begin{bmatrix} 0.970 & 0 & 0 \\ 0 & 0.020 & 0 \\ 0 & 0 & 0.010 \end{bmatrix} - \begin{bmatrix} 0.941 & 0.019 & 0.010 \\ 0.019 & 0.000 & 0.000 \\ 0.010 & 0.000 & 0.000 \end{bmatrix}$$
$$= \begin{bmatrix} 0.029 & -0.019 & -0.010 \\ -0.019 & 0.020 & -0.000 \\ -0.010 & -0.000 & 0.010 \end{bmatrix}$$

Los valores pequeños indican poca sensibilidad: Setosa está "saturada" — mover la flor poco cambia la predicción.

---

### Tema 26 | Hessiano (La curvatura del espacio de clasificación)

**🌸 Dummies**
El *Hessiano* es la matriz de segundas derivadas de una función escalar. Mide la *curvatura*: si es definido positivo en un punto, ese punto es mínimo local; si es indefinido, es punto de silla.
En el Iris: el Hessiano de la función de pérdida de un clasificador nos dice si el proceso de optimización converge (mínimo) o puede atascarse. El Hessiano de la distancia de Mahalanobis es exactamente $2\Sigma^{-1}$.

**∑ Algebraico**
Hessiano y criterio de segundo orden:
$$H(f)(x) = \left[ \frac{\partial^2 f}{\partial x_i \partial x_j} \right] \in \mathbb{R}^{n \times n}$$
Siempre simétrico si $f \in C^2$ (Teorema de Schwarz).
Criterio de segundo orden:
$\nabla f(x^*) = 0$ y $H$ def. positiva $\to$ mínimo local
$\nabla f(x^*) = 0$ y $H$ def. negativa $\to$ máximo local
$\nabla f(x^*) = 0$ y $H$ indefinida $\to$ punto de silla

Expansión de Taylor orden 2:
$$f(x+h) \approx f(x) + \nabla f(x)^T h + \frac{1}{2} h^T H(x) h$$

**🔢 Cálculo con el Iris**
Hessiano de la distancia euclídea y de Mahalanobis al cuadrado.
$f(x) = \|x - \mu_s\|^2 = \sum_i (x_i - \mu_{si})^2$
$\frac{\partial f}{\partial x_i} = 2(x_i - \mu_{si})$
$\frac{\partial^2 f}{\partial x_i^2} = 2, \quad \frac{\partial^2 f}{\partial x_i \partial x_j} = 0 \ (i \neq j)$
$H(\|x - \mu_s\|^2) = 2 \cdot I_4$
Eigenvalores: todos 2 $\to$ def. positiva ✓ (mínimo en $\mu_s$). Curvatura uniforme: igual en todas las direcciones.

$g(x) = (x - \mu_s)^T \Sigma_{\text{pooled}}^{-1} (x - \mu_s) \quad \text{[Mahalanobis}^2]$
$\nabla g = 2 \cdot \Sigma_{\text{pooled}}^{-1} \cdot (x - \mu_s)$
$H(g) = 2 \cdot \Sigma_{\text{pooled}}^{-1}$

Eigenvalores de $H(g) = 2 / \lambda_i(\Sigma_{\text{pooled}})$: Mayor curvatura en direcciones de menor varianza.
$\lambda_i(\Sigma_p) \approx [0.360, 0.135, 0.082, 0.032]$
$\lambda_i(H) = 2 / \lambda_i(\Sigma_p) \approx [5.56, 14.8, 24.4, 62.5]$
Interpretación: la Mahalanobis "estira" fuertemente las direcciones de poca varianza (más sensibles a diferencias).

---

## 📦 BLOQUE VII: ESPACIO DUAL

### Tema 27 | Espacio Dual (Los funcionales sobre el espacio Iris)

**🌸 Dummies**
El *espacio dual* $V^*$ es el espacio de todas las funciones lineales de $V$ a $\mathbb{R}$. Mientras los vectores de $V$ son "flores" (puntos 4D), los elementos del dual son "medidores": funciones que asignan un número a cada flor.
Por ejemplo, "toma la longitud del pétalo" es un funcional lineal — un elemento de $(\mathbb{R}^4)^*$. Cualquier combinación lineal de las 4 medidas también lo es. Los discriminantes lineales de Fisher son elementos del espacio dual.

**∑ Algebraico**
Espacio dual $V^*$ y base dual:
$$V^* = \{ \varphi : V \to \mathbb{R} : \varphi \text{ lineal} \} = \text{Hom}(V, \mathbb{R})$$
$\dim(V^*) = \dim(V) \quad \text{← mismo tamaño que } V$

Si $B=\{e_1, \dots, e_n\}$ es base de $V$, la base dual $B^*=\{e^1, \dots, e^n\}$ satisface:
$$e^i(e_j) = \delta_{ij} \quad \text{(delta de Kronecker)}$$

Todo $\varphi \in V^*$ se escribe como:
$\varphi = \varphi_1 e^1 + \dots + \varphi_n e^n \implies \varphi(v) = \sum_i \varphi_i v_i = \varphi^T v$

Isomorfismo natural (usando el producto escalar):
$V \cong V^* \quad \text{vía} \quad v \leftrightarrow \varphi_v = \langle v, \cdot \rangle$
(en $\mathbb{R}^n$ con producto estándar: $\varphi_v(u) = v^T u$)

**🔢 Cálculo con el Iris**
Funcionales lineales naturales del Iris. Los 4 funcionales base: $e^i(x) = x_i$
$e^1(x) = x_1 \quad \text{← "mide longitud sépalo"}$
$e^2(x) = x_2 \quad \text{← "mide ancho sépalo"}$
$e^3(x) = x_3 \quad \text{← "mide longitud pétalo"}$
$e^4(x) = x_4 \quad \text{← "mide ancho pétalo"}$

Funcional "índice pétalo total":
$\varphi_{pet} = e^3 + e^4 \in V^*$
$$\varphi_{pet}(\mu_s) = 1.462 + 0.246 = 1.708$$
$$\varphi_{pet}(\mu_{ve}) = 4.260 + 1.326 = 5.586$$
$$\varphi_{pet}(\mu_{vi}) = 5.552 + 2.026 = 7.578$$

¡Este funcional separa perfectamente las 3 especies! Setosa(1.7) $\ll$ Versicolor(5.6) $\ll$ Virginica(7.6).
Isomorfismo $V \cong V^*$: $\varphi_{pet} \leftrightarrow v_{pet} = [0, 0, 1, 1]^T \in V$
$$\langle v_{pet}, \mu_s \rangle = 0 \cdot 5.006 + 0 \cdot 3.428 + 1 \cdot 1.462 + 1 \cdot 0.246 = 1.708 \quad \text{✓}$$

---

### Tema 28 | Base Dual y Aniquilador (Lo que no miden los funcionales)

**🌸 Dummies**
El *aniquilador* de un subespacio $W$ es el conjunto de funcionales del dual que dan cero sobre todos los vectores de $W$. Son los "medidores ciegos" a $W$.
Para el Iris: el aniquilador de $\text{span}\{\mu_s\}$ son todos los funcionales que asignan valor cero a la media de Setosa. Estos funcionales no pueden "ver" la dirección de Setosa.

**∑ Algebraico**
Aniquilador $W^0$ de un subespacio $W$:
$$W^0 = \{ \varphi \in V^* : \varphi(w) = 0 \ \forall w \in W \}$$

Relación dimensional:
$$\dim(W^0) = \dim(V) - \dim(W)$$
$(W_1+W_2)^0 = W_1^0 \cap W_2^0$
$(W_1 \cap W_2)^0 = W_1^0 + W_2^0$
$W^{00} = W \quad \text{← reflexividad}$
Conexión con el complemento ortogonal: Vía el iso $V \cong V^*$: $W^0 \leftrightarrow W^\perp$.

**🔢 Cálculo con el Iris**
Aniquilador de $\text{span}\{\mu_{\text{setosa}}\}$:
$W = \text{span}\{\mu_s\} = \text{span}\{[5.006, 3.428, 1.462, 0.246]^T\}$
$W^0 = \{ \varphi=(\varphi_1, \varphi_2, \varphi_3, \varphi_4) : 5.006\varphi_1 + 3.428\varphi_2 + 1.462\varphi_3 + 0.246\varphi_4 = 0 \}$
$\dim(W^0) = 4 - 1 = 3$

Base de $W^0$ (3 funcionales que anulan $\mu_s$), fijando distintas variables libres:
$\varphi_1 = (-0.685, 1, 0, 0) \quad \text{← "ancho sépalo relativo"}$
$\varphi_2 = (-0.292, 0, 1, 0) \quad \text{← "longitud pétalo relativa"}$
$\varphi_3 = (-0.049, 0, 0, 1) \quad \text{← "ancho pétalo relativo"}$

Verificación $\varphi_1(\mu_s) = 0$:
$$(-0.685) \cdot 5.006 + 1 \cdot 3.428 + 0 \cdot 1.462 + 0 \cdot 0.246 = -3.429 + 3.428 \approx 0 \quad \text{✓}$$

¿Qué valor dan en las otras especies?
$$\varphi_1(\mu_{ve}) = -0.685 \cdot 5.936 + 1 \cdot 2.770 = -4.066 + 2.770 = -1.296$$
$$\varphi_1(\mu_{vi}) = -0.685 \cdot 6.588 + 1 \cdot 2.974 = -4.513 + 2.974 = -1.539$$
$\varphi_1$ sí distingue Versicolor de Virginica aunque sea "ciego" a Setosa.

---

## 📦 BLOQUE VIII: TENSORES

### Tema 29 | Producto Tensorial (Combinando dos espacios en uno mayor)

**🌸 Dummies**
El *producto tensorial* $V \otimes W$ crea un espacio que captura todas las interacciones entre elementos de $V$ y $W$. Si $V$ tiene dimensión 4, entonces $V \otimes V$ tiene dimensión 16 y captura todas las interacciones pareadas de variables.
La matriz de covarianza es exactamente un tensor de rango $(0,2)$: vive en $V^* \otimes V^*$ y mide la interacción (covarianza) entre cada par de variables. Los 16 números de $\Sigma$ son las componentes del tensor.

**∑ Algebraico**
Producto tensorial y tensores de rango $(p,q)$:
$$\dim(V \otimes W) = \dim(V) \cdot \dim(W)$$
Producto simple $v \otimes w \in V \otimes W$:
$$(v \otimes w)(\varphi, \psi) = \varphi(v) \cdot \psi(w)$$
Base de $V \otimes V$: $\{e_i \otimes e_j\} \to n^2$ elementos.
Un tensor $T \in V \otimes V$: $T = \sum_{ij} T_{ij} e_i \otimes e_j$.

Tipos de tensor $(p,q)$: $p$ índices contravariantes (arriba), $q$ índices covariantes (abajo).
Vector $v \in V$: tipo $(1,0) \quad \text{← 1 índice arriba}$
Funcional $\varphi \in V^*$: tipo $(0,1) \quad \text{← 1 índice abajo}$
Covarianza $\Sigma \in V^* \otimes V^*$: tipo $(0,2) \quad \text{← 2 índices abajo}$

**🔢 Cálculo con el Iris**
$\Sigma_{\text{total}}$ como tensor $(0,2)$: componentes y correlaciones.
$\Sigma = \sum_{ij} \sigma_{ij} e^i \otimes e^j$
Variables: 1=sep.len, 2=sep.wid, 3=pet.len, 4=pet.wid.

Componentes más significativas del tensor:
$\sigma_{33} = 3.1163 \quad \text{← mayor varianza (pet.len)}$
$\sigma_{13} = 1.2743 \quad \text{← mayor covarianza cruzada (sep-pet len)}$
$\sigma_{34} = 1.2956 \quad \text{← covarianza pétalo-pétalo}$
$\sigma_{11} = 0.6857 \quad \text{← varianza sep.len}$

Correlaciones (tensor normalizado):
$$r_{34} = \frac{\sigma_{34}}{\sqrt{\sigma_{33} \cdot \sigma_{44}}} = \frac{1.2956}{\sqrt{3.1163 \cdot 0.5810}} = \frac{1.2956}{1.3453} = 0.963 \quad \text{← ¡casi perfecta!}$$
$$r_{13} = \frac{1.2743}{\sqrt{0.6857 \cdot 3.1163}} = \frac{1.2743}{1.4622} = 0.872$$
$$r_{23} = \frac{-0.3297}{\sqrt{0.1900 \cdot 3.1163}} = \frac{-0.3297}{0.7697} = -0.428$$

El tensor de correlaciones tiene estructura clara:
* pétalos entre sí: correlación casi perfecta ($0.963$)
* sépalo-pétalo longitud: correlación alta ($0.872$)
* ancho sépalo: correlación negativa con pétalos ($-0.43$)

---

### Tema 30 | Transformación Tensorial y Cambio de Base

**🌸 Dummies**
La distinción entre tensores covariantes (índices abajo) y contravariantes (índices arriba) define cómo se transforman sus componentes cuando cambias de sistema de coordenadas.
Para el Iris: si cambiamos de centímetros a milímetros en las variables de pétalo, las componentes de la covarianza se transforman de forma covariante — los números cambian pero la geometría descrita es la misma.

**∑ Algebraico**
Reglas de transformación bajo cambio de base $P$ (Base nueva: $e'_a = P^i_a e_i$):
Vector $(1,0)$ — contravariante: $(v')^a = (P^{-1})^a_i v^i$
Funcional $(0,1)$ — covariante: $\varphi'_a = P^i_a \varphi_i$
Tensor $(0,2)$ covariante (como la covarianza $\Sigma$):
$$\Sigma'_{ab} = P^i_a \cdot P^j_b \cdot \Sigma_{ij}$$
En notación matricial: $\Sigma' = P^T \cdot \Sigma \cdot P$
Tensor $(1,1)$ mixto (como transformación lineal $T$):
$$T'^a_b = (P^{-1})^a_i \cdot P^j_b \cdot T^i_j$$
En notación matricial: $T' = P^{-1} \cdot T \cdot P$ (matrices semejantes).

**🔢 Cálculo con el Iris**
Transformación de $\Sigma$ bajo cambio de unidades (cm $\to$ mm en pétalos):
Cambio: $x_3, x_4$ pasan de cm a mm $\to$ se multiplican por 10.
Matriz de cambio de base $P = \text{diag}(1, 1, 10, 10)$.

$\Sigma_{\text{total}}$ transforma como tensor $(0,2)$: $\Sigma' = P^T \Sigma P = P \Sigma P$ ($P$ simétrica).

Bloques afectados ($\times10$ un factor, $\times100$ dos factores):
$\Sigma'_{11} = 1 \cdot 1 \cdot 0.686 = 0.686 \quad \text{← sépalo-sépalo: sin cambio}$
$\Sigma'_{13} = 1 \cdot 10 \cdot 1.274 = 12.74 \quad \text{← sépalo-pétalo: } \times10$
$\Sigma'_{33} = 10 \cdot 10 \cdot 3.116 = 311.6 \quad \text{← pétalo-pétalo: } \times100$
$\Sigma'_{34} = 10 \cdot 10 \cdot 1.296 = 129.6 \quad \text{← pétalo-pétalo: } \times100$
$\Sigma'_{44} = 10 \cdot 10 \cdot 0.581 = 58.1 \quad \text{← pétalo-pétalo: } \times100$

Verificación: las correlaciones son invariantes al cambio de unidades:
$$r'_{34} = \frac{129.6}{\sqrt{311.6 \cdot 58.1}} = \frac{129.6}{134.5} = 0.963 = r_{34} \text{ original} \quad \text{✓}$$

> **🔑 Conclusión del Bloque VIII:** La covarianza del Iris es un tensor de tipo $(0,2)$. Sus componentes numéricas dependen del sistema de coordenadas, pero las invariantes geométricas (correlaciones, eigenvalores, distancias de Mahalanobis) son independientes de las unidades elegidas.
