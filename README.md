<h1 style="color: rgb(20,100,200)"> Ajuste de curva usando funções de base radial </h1>
<p>Este é um projeto de ciência de dados cujo objetivo era ajustar os dados em uma curva usando funções de base radial</p>


> Status: Completado


<p>os dados foram tirados do site <a href = "https://globalsolaratlas.info/detail?c=-14.349548,36.650391,4&s=-18.312811,48.251953&m=site">https://globalsolaratlas.info/detail?c=-14.349548,36.650391,4&s=-18.312811,48.251953&m=site</a></p>

#**Ajuste de curva utilizando funções de base radial**

Dado um conjunto de pontos no plano cartesiano

$$
C = \{\ (x_1,y_1),(x_2,y_2),...,(x_n,y_n) \}\
$$

queremos uma curva que melhor se ajuste aos pontos, ou seja, queremos escrever os valores $y$ como uma combinação linear de funções

$$
y_i \approx \sum_{j = 0}^{M} \alpha_j f_j(x_i)
$$

para todo ponto no conjunto C.
ou seja, queremos minimizar a diferença entre o valor real e o valor dado pela função, podemos minimizar então o erro médio quadrático entre as duas variáveis

$$
\text{Minimize } ||y_i - \sum_{j = 0}^{N} \alpha_j f_j(x_i) ||_{2} ^2
$$

Podemos ainda escrever como um sistema de equações lineares, e assim temos

$$
\begin{cases}
y_1 &= \sum_{j = 0}^{M} \alpha_j f_j(x_1) = \alpha_1 f_1(x_1) + \alpha_2 f_2(x_1) + ... + \alpha_n f_n(x_1)\\
y_2 &= \sum_{j = 0}^{M} \alpha_j f_j(x_2)= \alpha_1 f_1(x_2) + \alpha_2 f_2(x_2) +  ... + \alpha_n f_n(x_2) \\
&\vdots \\
y_n &= \sum_{j = 0}^{M} \alpha_j f_j(x_n) = \alpha_1 f_1(x_3) + \alpha_2 f_2(x_3) + ... + \alpha_n f_n(x_3)
\end{cases}
$$

Podemos representá-lo na forma matricial como:

$$
\mathbf{Y} = \mathbf{F} \boldsymbol{\alpha}
$$

Onde:

$$
$\mathbf{F} = \begin{bmatrix}
f_1(x_1) & f_1(x_1) & \cdots & f_M(x_1) \\
f_1(x_2) & f_1(x_2) & \cdots & f_M(x_2) \\
\vdots & \vdots & \ddots & \vdots \\
f_1(x_n) & f_1(x_n) & \cdots & f_M(x_n)
\end{bmatrix}$
$$

é a matriz das funções de base.

$$
$\boldsymbol{\alpha} = \begin{bmatrix}
\alpha_1 \\
\alpha_2 \\
\vdots \\
\alpha_M
\end{bmatrix}$
$$
é o vetor de coeficientes.

$$
$\mathbf{Y} = \begin{bmatrix}
y_1 \\
y_2 \\
\vdots \\
y_n
\end{bmatrix}$ 
$$

é o vetor de variáveis dependentes.


e agora nossa função objetivo se torna

$$
J(\vec{ \alpha} ) = ||y_i - \sum_{j = 1}^{M} \alpha_j f_j(x_i) ||_{2} ^2
$$

fazendo agora sua derivada em relação ao k-ésimo coeficiente $\alpha_k$, temos

$$
\frac{\partial }{\partial \alpha_k} J(\vec{ \alpha} ) = \frac{\partial }{\partial \alpha_k}  \sum_{i = 0 }^{N-1} ( y_i - \sum_{j = 1}^{M} \alpha_j f_j(x_i))^2
$$

aplicando a regra da cadeia

$$
\frac{\partial }{\partial \alpha_k} J(\vec{ \alpha} ) = - \sum_{i = 0 }^{N-1} 2 ( y_i - \sum_{j = 1}^{M} \alpha_j f_j(x_i)) \cdot  \frac{\partial }{\partial \alpha_k}\sum_{j = 1}^{M} \alpha_j f_j(x_i)
$$

então finalmente temos

$$
\frac{\partial }{\partial \alpha_k} J(\vec{ \alpha} ) = - \sum_{i = 0 }^{N-1} 2 ( y_i - \sum_{j = 1}^{M} \alpha_j f_j(x_i))  f_k(x_i) = 0
$$

agora dividindo a equação por $-2$ e rearranjando os termos de cada lado, temos

$$
\sum_{i = 0 }^{N-1}  y_i f_k(x_i) = \sum_{i = 0 }^{N-1} \sum_{j = 1}^{M} \alpha_j f_j(x_i)  f_k(x_i) = 0
$$

que pode ser visto, matricialmente como

$$
\mathbf{F}^T \mathbf{y} = \mathbf{F}^T \mathbf{F \alpha} 
$$

então o vetor de coordenadas $\mathbf{\alpha}$ será

$$
\mathbf{\alpha} = (\mathbf{F}^T \mathbf{F})^{-1} \mathbf{F}^T \mathbf{y}
$$

que é conhecida como solução pseudo inversa, devido a matriz pseudo inversa

$$
F^{+} = (\mathbf{F}^T \mathbf{F})^{-1} \mathbf{F}^T
$$

onde o i-ésimo,j-ésimo termo da matriz $\mathbf{F}$ é dado por

$$
F_{ij} = f_j(x_i)
$$

é a j-ésima função aplicada no i-ésimo ponto.


##**Funções de base radial**
As funções de base radial são funções que formam uma base que conseguem ajustar quaisqueis pontos
A função de base radial escolhida para ajustar o conjunto de dados abaixo foi a inversa multiquadrica, dada por

$$
\phi(x,c,\sigma) = \frac{1}{\sqrt{1 + \sigma^2 (x-c)^2}}
$$

o vetor de centros e os valores de sigma podem ser escolhidos empiricamente, mas com cuidado.
