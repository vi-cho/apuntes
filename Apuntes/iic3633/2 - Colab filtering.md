# Limitaciones de user k-NN
Este método sifre de un problema de balance entre escalabilidad y exactitud. Cuando aumentamos la cantidad de vecinos calculados, la exactitud de la predicción debería aumentar. Sin embargo, cuando aumentamos la cantidad de usuarios disponibles, aumenta también el costo de encontrar los k vecinos, ya que k-NN es $O(dnk)$. Si tenemos un sitio con millones de usuarios, calcular las recomendaciones con un modelo memory-based se vuelve insostenible.

Además, surgen otros problemas, como la dispersión

# item k-NN
Una forma de solucionar estos problemas, es invertir el cálculo de la similitud hacia los items, en vez de evaluar a cada usuario. Esto remplaza la matriz usuarios x items por una matriz items x items