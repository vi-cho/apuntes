# El problema
Complejidad agregada a un problema clásico de IA: Puedo encontrar un elemento que pertenece a una categoría, pero ahora tengo que determinar si a un usuario le va a gustar el elemento encontrado

Si tengo un dataset de un usuario con elementos que le ha gustado anteriormente, puede 

# Definición
Un sistema de recomendación (RecSys) es un sistema que busca ayudar a un usuario o grupo de users a elegir elementos de un set muy numerosos o un amplio espacio de información. Burke le agrega de forma personalizada a esta definición.

Los sistemas recomendadores son increíblemente útiles y populares en toda clase de aplicaciones y servicios *mainstream*, implementados principalmente en motores de búsqueda y recomendaciones en base a actividad previa del usuario. De aquí salen grandes ejemplos como el "Users like you also bought" de Amazon, las recomendaciones de YouTube, la búsqueda de Google, etc.

Matemáticamente, un RecSys es un problema de optimización de la siguiente forma:

$$\begin{aligned}
\forall c \in C = \quad &\arg\max_{s\in S} u(c,s)\\
u: C\times S \rightarrow R:\quad & \text{Función de utilidad}\\
R: \quad &\text{Conjunto recomendado de items}\\
C: \quad &\text{Conjunto de usuarios}\\
S: \quad &\text{Conjunto de items}
\end{aligned}$$
Las primeras implementaciones de lo que hoy son los RecSys nacen en Xerox PARC con un servicio de email Tapestry, luego se crea MovieLens, una base de datos de distintas versiones (1k, 100k, 1M) que almacena usuarios con peliculas y su rating, el cual se usa para testear algoritmos de recomendación. Eventualmente, Netflix organiza el NetflixPrize para encontrar el mejor algoritmo de filtración colaborativa, ofreciendo 1M USD al equipo ganador. Hoy en día, los RecSys son ampliamente utilizados por diversas compañias y servicios dedicados a cualquier cosa.

Antes de RecSys orientado a usuarios, se usaba el Ranking No Personalizado, el cual decide que recomendar en base a la popularidad de los elementos. Esta forma sufre de la regla del 80/20, donde el 20% más popular de los items se lleva el 80% de las interacciones totales, por lo que se pierde la oportunidad de recomendar elementos que pueden ser más afines a un usuario en especifico, pero que no son tan populares.

SI queremos categorizar los tipos de RecSys, surgen dos meta-categorías: Data-based y Model-based categories. Cuando categorizamos los sistemas por el uso de los datos, podemos distinguir entre sistemas rule-based, content-based y collaborative filtering. La categorización en base al modelo se parece mucho a la clasificación de AI, y podemos distinguir sistemas memory-based (k-NN,  SVM's) o model-based (Arboles, NeuNet).

# a
Si tomamos el problema y lo simplificamos, podemos representarlo como un modelo que busca predecir el rating que un usuario x puede darle a un item m en base a sus ratings observados anteriormente. Con este framing resalta una complicación importante que dificulta la predicción: los usuarios no interactúan con los items generalmente. Para anotar los datos de los usuarios, se crea una matriz de usuarios x items, donde cada entrada indica el rating dado. Esta tabla se llena generalmente con un 5% de los datos totales.

La predicción se puede calificar con la ecuación:
$$sda$$
# Filtrado Colaborativo basado en usuario
También llamado user-kNN, corresponde a una estrategia para predecir los ratings de un usuario. Lo que hace este modelo es 1) Encontrar los k vecinos más cercanos al usuario que queremos predecir, a través de una función de similaridad arbitraria $w(a,i)$. Luego, pasamos al paso 2) Predecir el rating del usuario a sobre un item j con la función:
$$p_{a,j}= v_a+a\sum_{i=1}^{n}w(a,i)(v_{i,j}-v_i) $$
## Ejemplo: Correlación de Pearson
Imaginemos una situacion donde hay un usuario activo y 3 otros usuarios. Para usar user k-NN, primero encontramos los usuarios más cercanos a nuestro usuario activo. Usando correlación de Pearson, con fórmula:
$$Sim(u,n)$$
vemos que los usuarios 1 y 2 son los más cercanos a nuestro usuario. Luego, tenemos 3 items que nuestro usuario activo no ha visto, pero que los otros 2 sí han visto. Con esto, podemos calcular una predicción del rating que nuestro usuario asignaría en base a la similaridad de los otros usuarios y los ratings que han asignado:
$$pred(u,i)=r_u+\frac{\sum_{n\subset neighbors(u)}userSim(u,n)\cdot(r_{n,i}-r_n)}{\sum_{n\subset neighbors(u)}userSim(u,n)}$$. Así, los usuarios más similares a nuestro usuario tienen un peso mayor sobre la predicción que otros usuarios con similitudes más bajas.
### Paréntesis de IA
Cuando tenemos un dataset, este se separará entre un set de train y un set de testeo. En el caso de RecSys, hay que ser cuidadosos con como se eligen los datos de training y testeo, ya que debo tener datos de los mismos usuarios en ambas particiones; si tengo un usuario en testeo que nunca vi en training, el modelo tendrá que adivinar al achunte, por lo que se debe hacer un muestreo que distribuya a los usuarios entre testing y training. Además, la partición de train en realidad es de training + validation. En esta etapa, donde se valida, es donde se deben optimizar los hiperparámetros, o sea, aquí es donde se elige la cantidad de vecinos a usar en el modelo k-NN

## Pros y contras
Pro:
- Muy simple de implementar
- Agnóstico al contenido
	- Estas dos salen porque el método se basa en los ratings de usuarios previos, y no depende de si estas recomendando películas, canciones, libros, etc.
- Es más preciso que otras técnicas de recomendación
	- Un poco outdated, con deep learning.
- Además, existe item k-NN, que resuelve el problema de la lentitud de user k-NN
Contra:
- Sparsity
- COld start
- New Item
Debido a las características de los contras del ColabFilter, generalmente estos se mezclan con otras técnicas que permiten aliviar estos problemas.
