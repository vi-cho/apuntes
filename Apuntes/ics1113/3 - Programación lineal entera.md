# Problemas lineales enteros (ILP)

Hasta ahora, hemos visto problemas con variables continuas. En general se trabaja mucho con variables que son enteras(discretas). En vez de tener variables $x\in\mathbb{R}^n$, vamos a encontrar variables de la forma $x\in\mathbb{R}^n//x_j\in\mathbb{Z},\forall j\in J$, donde algunas variables son enteras.

Principalmente esto se manifiesta en problemas con variables binarias, que determinan decisiones *a la* Bernoulli, como si enviar cierto producto o no.

## Knapsack problem

El problema consiste en encontrar la forma óptima de organizar una mochila con objetos n.

Los parámetros que tenemos son:
- Conjunto n de objetos a almacenar
- aj >0 peso del objeto j
- cj > 0 beneficio de llevar objeto
- b > 0 capacidad máxima de la mochila
La pregunta es qué objetos metemos en la mochila, por lo que tenemos una variable de decisión binaria, que vale 1 si queremos ingresar el objeto j a la mochila y 0 en caso contrario.
$$\begin{align}x_j\in\{0,1\} 
\begin{cases}
1&\text{si y solo si se incluye al objeto}\\0& \text{en caso contrario}
\end{cases} \quad&\forall j\in\{1,...,n\}
\end{align}$$
Luego, tenemos una sola restricción que limita la cantidad máxima de objetos a ingresar
$$\begin{align}\sum_{j=1}^{n}a_jx_j\leq b\end{align}$$
Y finalmente escribimos una función objetivo que maximize el beneficio por incluir objetos
$$\begin{align}\max\quad&\sum_{j=1}^{n}c_jx_j\end{align}$$
Volvemos a escribir todo de manera compacta:
$$\begin{align}
\max\quad&\sum_{j=1}^{n}c_jx_j\\
s.t\quad&\sum_{j=1}^{n}a_jx_j\leq b\\
\quad&x_j\in\{0,1\}\quad&\forall j\in\{1,...,n\}
\end{align}$$
# Restricciones lógicas
Las variables binarias particularmente nos dan a libertad de integrar restricciones lógicas i.e. a AND b, a OR b, etc. a nuestros modelos de optimización. A continuación se enumeran las opciones disponibles:
- si xa entonces xb: 