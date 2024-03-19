# Introducción
Para efectos del curso, un computador es una máquina *programable* que ejecuta programas.

Un computador necesitará estos elementos para lograr su función:
- Datos que manipular
- Operaciones para manipular datos
- Variables para almacenar datos
- Control de flujo
En primer lugar, veremos como se representan datos en un computador
# Representación de números
Con números se puede codifcar distintos tipos de datos, como texto, imágenes, videos, etc

Si queremos aprovechar esto en un computador, debemos encontrar como representar números usando las herramientas que tenemos disponibles.

Primero, tenemos que los números en el día a día se representan de forma **posicional**, donde se elige una base en función a la cantidad de símbolos disponibles para escribir, donde cada numero $y$ en posición $x$ dentro del número significa $y\cdot b^x$, para una base $b$ cualquiera. En un computador, nos sirve usar la base binaria ya que podemos representar números como presencia o ausencia de electricidad, la cual será escrita *as is*, o con un subíndice b, de la forma XXXXb. También se usa hexadecimal por su facil conversión a 4 bits, lo que condensa numeros grandes. Se escribe 0xYYYY, o bien YYYYh.

Para pasar de hexa a bin y viceversa, se debe separar lo binario en 4 bits y representar cada bit como un numero hex y concatenar. Los 4 bits nacen naturalmente por el mapeo entre un número binario y su representación en hex.

## Números negativos
En los números clásicos, cuando queremos escribir números negativos usamos un símbolo extra al sistema 0-9, que denota el signo del número. Sin embargo, cuando trabajamos con computadores, no tenemos el lujo de agregar símbolos, ya que trabajamos con electricidad.

Para solucionar esto, existen varias opciones. Lo que más nos importa es que se cumpla que $n + (-n) = 0$ para todo número. Esto descarta opciones como usar el bit más significativo como signo. La opción que usaremos será la del **complemento de dos**,
donde por definición $\forall n, -n = \neg n$ o bién, cada número positivo encuentra su negativo en una versión flipped de cada bit y se suma 1, ignorando bits de sobra. Entonces, si tenemos que $1 = 0001 \Rightarrow -1 = 1111$ y $1 + (-1) = 0001 + 1111 = 10000 = 0000$. Siempre se asumirá que los números binarios se escriben en complemento de 2, a menos que se indique lo contrario. Una forma fácil de encontrar el complemento es encontrar el primer bit 1 del número, dejar intacto lo que viene antes del bit y sacar complemento para atrás.

Esta representación sufre de ciertos problemas. En primer lugar, esta desbalanceada ya que existe un número negativo más que los positivos, porque el cero usa el bit positivo (i.e. en 4 bits, se representa desde el -8 al 7). Además, podemos sufrir de overflow cuando hacemos una operación que se escapa del rango de representación (i.e. $0111b(7) + 0001b(1) = 1000b = -8 \neq 8$, el nivel 255 + 1 de pacman)