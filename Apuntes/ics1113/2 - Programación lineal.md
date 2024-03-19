# Modelación lineal continua (LP)
Como se vio [[ics1113/1 - Introducción#Forma canónica|anteriormente]], un modelo siempre se puede representar por su forma canónica.

Cuando hablamos de un modelo LP (linear programming), podemos definirlo en función a restricciones sobre la forma canónica. En este caso, $f(x), h(x), g(x)$ deben ser lineales, y se debe cumplir que $x\subseteq\mathbb{R}^n$(x es continuo). Un ejemplo:
$$
\begin{equation}\begin{aligned}
\min_{x_{1},x_{2}}\quad& 800x_1+500x_2\\
s.t\quad& 20x_1+10x_2\leq 2500\\
\quad& 250x_1+500x_2\leq 50000\\
\quad& x_1,x_2\geq0
\end{aligned}\end{equation}
$$
Este modelo tiene 2 variables y 4 restricciones, con solución y valór óptimo: $x^*=(100,50), v^x=105000$. 

Este tipo de problemas pueden ser representados gráficamente, tomando como ejes las variables y con lineas que representan las restricciones. Así, es fácil ver que el propósito de las restricciones es delimitar el dominio de soluciones factibles para el vector $x$. Cuando se tiene este dominio, es necesario encontrar el punto $x^*$ donde la función objetivo encuentra su valor mínimo/máximo.

## Problema de la dieta
Este es uno de los primeros problemas de LP, donde se busca crear una dieta para tropas que minimizara el costo de producción, considerando las necesidades calóricas y nutritivas de un soldado promedio. La definición de este modelo ilustra la forma en la que se formula generalmente un problema LP.

En primer lugar se define la información que existe dentro del problema. En el caso de la dieta, se dispone de varios alimentos numerados $\{1,...,n\}$. Cada uno de estos posee un precio por unidad $c_j\in\mathbb{R}⁺$, con $j\in\{1,..,n\}$ . También, tenemos que existen $m$ nutrientes, que poseen una cantidad mínima y máxima de consumo diario, que podemos definir como $a_i:i\in\{1,...,m\}$ y $b_i:i\in\{1,...,m\}$. Finalmente, cada alimento $j$ debe tener un aporte nutricional $p$ para cada nutriente $i$, lo que definimos como $p_{ij}:i\in\{1,...,m\},j\in\{1,...,n\}$

Luego, definimos que variables se deben decidir en el problema. Para este caso, tenemos que la cantidad de alimento es la variable a controlar; la definimos como el vector $x=(x_1,...,x_n)^T\in\mathbb{R}⁺$. Con esto, podemos definir una función objetivo, que entregue un valor que nos gustaría minimizar o maximizar. En este caso, la función nace naturalmente como el costo total de comprar cada alimento: $\min_{x}\sum_{j=1}^{n}c_jx_j$. Finalmente, podemos definir ecuaciones de restricción, que relacionan a las variables con los parámetros definidos anteriormente. Para optimizar la dieta, debemos delimitar las condiciones nutritivas que queremos satisfacer, entonces salen las siguientes restricciones
$$\begin{aligned}
x_j\geq0\quad&\forall j\in\{1,..,n\}\\
\sum_{j=1}^{n}p_{ij}x_{j}\leq b_{i}\quad&\forall i\in\{1,..,m\}\\
\sum_{j=1}^{n}p_{ij}x_{j}\geq a_{i}\quad&\forall i\in\{1,...,m\}
\end{aligned}$$
Así, tenemos todos los componentes para escribir matemáticamente un modelo.

## Problema de producción e inventario
El desarrollo de este problema ilustra una estrategia para modelar condiciones que se pueden almacenar o extender a través de un periodo de tiempo.

Si queremos optimizar la producción de un producto en un horizonte de T periodos, asumiendo una bodega inicial vacía, podemos identificar los siguientes parámetros en cada periodo $t = \{1,...,T\}$:
- $d_t$: demanda
- $c_t$: costo unitario de producción
- $h_t$: costo unitaro de inventario
- $k_t$: capacidad productiva
Así, podemos optimizar la pregunta de cuánto producir, almacenar y vender en cada periodo T.

Si analizamos un periodo $t$ en particular, podemos notar que lo que venda y produzca para ese periodo se ve afectado por lo que almacené en $t-1$, y lo que almacenemos afectará a $t+1$. Así, tenemos que en el periodo $t$ tenemos una demanda $d(t)$ que debemos cumplir, una producción $x(t)$ que puedo producir, y que junto al inventario $z(t-1)$ deben satisfacer la demanda, y un inventario $z(t)$ que almacena lo que sobra entre la producción y el inventario luego de satisfacer $d(t)$.

Ahora, podemos determinar variables de decisión que nacen naturalmente de este análisis. En primer lugar, debemos decidir la cantidad a producir en $t$, y una variable opcional de cuanto guardar en inventario. Esta segunda variable no es necesaria, ya que estaría definida por la resta entre la producción total - la demanda del día, pero enunciarla ayuda con la claridad del problema.

- $x_t\geq 0:t\in\{1,...,T\}$
- $z_t\geq 0:t\in\{1,...,T\}$

Así, pasamos a definir las restricciones del problema. 

1) Debemos restringir el balance del inventario, ya que debemos limitar el espacio y eliminar situaciones imposibles, como que haya más inventario del que sobró en un día.
$$\begin{align}
z_t=z_{t-1}+x_t-d_t\quad& \forall t \in \{2,...,T\}\\
z_1=x_1-d_1\quad&
\end{align}$$
La gracia de definir esta relación es que nos permite producir más de lo que se pide en un día determinado, así podemos optimizar la producción y hacer la mayor cantidad de productos posibles todos los días.

2) Restringimos la capacidad productiva para cada día
$$\begin{align}x_t\leq k_t\quad&\forall t\in\{1,...,T\}\end{align}$$
FInalmente, vemos la función objetivo. Como queremos maximizar el profit de nuestra operación, esta nace naturalmente como minimizar los costos de producción y los de almacenamiento.
$$\begin{align}\min\quad& \sum_{t=1}^{T}c_tx_t+\sum_{t=1}^{T}h_tz_t\end{align}$$
Así, escribimos el modelo completo
$$\begin{align}\min\quad& \sum_{t=1}^{T}c_tx_t+\sum_{t=1}^{T}h_tz_t\\
s.t.\quad& z_t=z_{t-1}+x_t-d_t\quad&\forall t\in\{2,...,T\}\\
\quad& z_1=x_1-d_1\\
\quad& x_t\leq k_t\quad&\forall t\in\{1,...,T\}\\
\quad& x,z\geq0
\end{align}$$
