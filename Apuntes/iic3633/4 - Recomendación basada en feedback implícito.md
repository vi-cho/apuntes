# Feedback
Los métodos estudiados anteriormente se basan en el feedback explícito, ya que reqiueren que el usuario ponga un rating, una nota o calificación al item que estan consumiendo. El modelo recomendador funciona a base de una retroalimentación entregada por el usuario explícita. Hay algunos problemas con este tipo de feedback, uno notable es que pueden haber grandes diferencias entre lo que indica el usuario a través de reseñas o calificaciones  y lo que finalmente el usuario consume. También, la señal explícita es difícil de obtener, ya que la mayoría de los usuarios simplemente no entregan feedback, a menos que la experiencia haya sido notablemente pésima o excelente.

# Implicidad
Para solucionar esto, podemos tomar ciertas métricas y 

# Características
- Es más facil de obtener
- No contiene información negativa
- Contiene ruido
- No usa métricas de error como RMSE o MAE, por lo que debemos usar nuevas métricas de ranking
# Métodos particulares
## Alternating least squares (ALS)
### Weighted regularized matrix factorization
Adaptación de FunkSVD aplicado sobre una matriz de cantidad de clicks u otra métrica implícita, descirto por Yifan Hu

## Bayesian personalized ranking with matrix factorization

## Dwell time
Descrito en un paper por Yi Xi, considera el tiempo transcurrido en una página web a través de distintos dispositivos.

# ALS
El modelo permite aprender representaciones latentes de usuarios e items a partír de feedback implícito, escalar la cantidad de users e ítems paralelizando el entrenamiento con Mínimos cuadrados alternados.

## Modelando IF
En primer lugar, debemos representar matemáticamente la métrica, como por ejemplo, los clicks de un usuarios sobre un item
$$p_{ui} = \begin{cases}\end{cases}$$
El ruido de las métricas se integran con una variable de confianza, incorporada por un híperparámetro que indica la tasa a la que crece la confianza con mayor cantidad de clicks (determinado empíricamente):
$$c_{ui}=1+\alpha r_{ui}$$
$$c_{ui}=1+\alpha\log(1+r_{ui}/\epsilon)$$
Con esto, cambia nuestra función de pérdida en ALS
$$\min_{x,y}\sum_{u,i}c_{ui}(p_{ui}-x_u^Ty_i)^2+\lambda(\sum_u||x_u||²+\sum_{i}||y_i||²)$$
## ALS vs FunkSVD
1) FunkSVD esta desarrollado para explícita, pero se podría usar con datos implícitos
2) ALS supera a FunkSVD con datos implícitos debido a l
3) La evaluación de error en ALS se hace con métricas de Ranking
4) ALS

## Paralelización del cálculo


## Uso IRL
Con implicit en python se puede usar ALS
![[Recording 20240319120431.webm]]
