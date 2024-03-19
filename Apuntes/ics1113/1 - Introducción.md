# Optimización
La optimización es una rama/disciplina de la investigación de operaciones, un área de la ciencia que busca resolver problemas usando matemática. En opti, se busca la selección determinística del mejor elemento en un conjunto disponible. *Una aplicación se ve en IIC2613*

# Modelos
El modelo es una representación de la realidad que resume las features más relevantes para entender un problema. Manipulando matemáticamente este modelo, podemos encontrar el/los escenarios óptimos de un problema. Generar modelos es un arte, donde se necesita creatividad para representar datos como parámetros, decisiones como variables y restricciones sobre estas variables como relaciones matemáticas.

## Forma canónica
En general, la forma canónica de un modelo se escribe como:

$$\begin{aligned}
\min_{x}\quad& f(x)\\
s.t\quad& h(x)=0\\
\quad& g(x)\leq 0\\
\quad& x\in\Omega :\Omega\subseteq\mathbb{R}^{n}
\end{aligned}$$
- $x\subseteq\mathbb{R}^n$= vector de variables
- $f(x)$: función objetivo
- $h(x)$: restricciones de igualdad
- $h(x)$: restricciones de desigualdad
- $\Omega$: dominio de las variables
## Más alla de la modelación
Luego de parender a modelar, se estudiará la teoría de la optimización, resolviendo temas como la existencia y unicidad de soluciones a modelos, propiedades de modelos específicos y equivalencia entre modelos alternativos para un mismo problema. Se verán métodos para optimizar modelos

## Taxonomía de modelos
Los modelos se separan en dos categorias: Lineales y No Lineales. La diferencia clave es que los modelos no lineales poseen relaciones no lineales entre variables, sea exponenciación y/o multiplicacion entre variables. Además, cada categoria se separa por modelos con variables discretas (números naturales) o continuas. En el curso se verá LP(lineal continup), NLP(no lineal continuo) y MIP(lineal discreto).