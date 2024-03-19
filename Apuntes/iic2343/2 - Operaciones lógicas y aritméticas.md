# Historia
Ahora que tenemos un sistema teórico para manipular bits, debemos mirar al pasado para entender como podemos pasar del papel al metal.

Los primeros computadores eran análogos, que procesaban señales continuas en forma de voltaje. Estas eran lentas, y sufrián de ruido y descalibraciones que afectaban la precisión de los resultados.

Shannon llega y demuestra que es más eficiente transformas fuentes de datos contínuos a bits para mantener precisión y una trnasmisión confiable.

Realizar esta transformación de o analógico a lo digital, se necesitan 3 elementos:
- Un sistema numérico eficiente (binario, lo tenemos)
- Un mecanismo para operar de forma eficiente sobre el sistema
- Componentes físicos que implementen este mecanismo

## Lógica booleana
Para pasar al segundo punto, debemos usar la lógica booleana. Shannon en un paper demuestra que esta lógica puede representarse con circuitos digitales, osea, podemos usar circuitos para realizar operaciones de lógica booleana.

En resumen, la LB requiere de variables o proposiciones lógicas que representen valores que pueden ser verdaderos o falsos. Esto es análogo a como funcionan los bits, y que puede representarse físicamente como presencia o ausencia de electricidad. Luego, LB necesita de conectores lógicos que puedan unir variables y las alteren según tablas de verdad. Esto es análogo a las operaciones aritméticas sobre bits.

Una ventaja de usar esta lógica es que podemos representar un lenguaje lógico completo con muy pocos conectores lógicos. Sólo usando los conectores AND, OR y NOT podemos representar todos los conectores posibles. Más aún, existen dos conectores NAND y NOR que son conocidos como conectores globales, ya que solo uniendo NANDs o NORs, podemos representar AND, OR y NOT.

### La suma
En primera instancia, necesitamos una forma de representar la suma de dos números de un bit. Podemos escribir una tabla que compara el resultado de una suma versus los dos bits, y ver que la tabla resulta ser idéntica a una tabla de verdad de XOR. Además, si queremos tener acarreo en esta suma, podemos ver que su tabla es idéntica a la tabla de verdad AND.

## Implementación
Ahora que tenemos un sistema para representar las operaciones de bits, debemos crear componentes físicos que puedan manipular la electricidad y emular el funcionamiento de estos conectores lógicos. Shannon nuevamente crea los Relays, un componente eléctrico que con una señal de control permite o interrupte el paso de la corriente eléctrica desde un input hacia dos outputs. 

Con este mecanismo, podemos representar a los 3 conectores lógicos fundamentales para generar un sistema completo. 

En primer lugar un NOT puede considerarse como un input A, y una de las salidas como NOT A cuando se recibe un input de control. 

Un OR se puede construir con 2 relays, donde se usan las salidas que se activan cuando pasa corriente por los inputs de control, por lo que en nuestro output habría corriente cuando haya inputs de control en alguno o ambos de los relays.

Finalmente, un AND se puede crear con dos relays en serie, donde la salida de un relay se conecta al segundo, y el voltaje pasaría sólo si ambas señales de control poseen corriente.

# Operaciones aritméticas digitales
Ahora que sabemos todo esto, podemos definir las operaciones aritméticas binarias en circuitos digitales. 

En primer lugar, sabemos que la suma de dos números de un bit se puede ver como una compuerta XOR y su acarreo como un AND. Podemos notar que la suma de x bits requerrirá una salida de x+1 bits, debido al acarreo que puede tener la suma. Con estos componentes podemos crear un Half Adder, que toma las entradas de A y B, conecta ambas a un XOR y un AND, y retorna dos salidas S y C, de suma y acarreo. Con 2 Half Adders puedo crear un Full Adder. Con esta construcción, podemos sumar dos números de 1 bit con un bit de carryover. Así, podemos extenderla, concatenando FA's para sumar números de mayores bits. Si queremos restar, la solución es generar un circuito que pueda convertir a B en su complemento de 2. Esto se logra negando todos los bits de B y hardcodeando a Cin = 1.

## Abstracción de componentes
Para facilitar la construcción de un computador (sobre todo en el proyecto), se hace necesario representar a los componentes de una forma más simplicada, ya que cada componente esta compuesto por unidades más pequeñas hasta llegar a sus circuitos lógicos. Con la notación de buses, podemos representar por ejemplo un sumador de 8 bits, como una caja negra con sus inputs y outputs finales, sabiendo que este sería una conexión de 8 full adders.

## Minterms y maxterms
Si se nos entrega una tabla de verdad cualquiera, y se nos pide generar un circuito que corresponda a esta tabla, hay un método más efectivo que construirlo a fuerza bruta. Si la tabla contiene principalmente 0's, entonces usamos *minterms*, donde nos centramos en la combinación de inputs que entregan 1, y combinamos las fórmulas lógicas con un OR, para finalmente traducir la fórmula matemática a un circuito lógico. En el caso donde los 1's son mayoría, usamos *maxterms* que es el mismo proceso, pero centrándonos en las combinaciones que entregan 0 y negando las fórmulas encontradas, concatenandolas con un AND.

![[Recording 20240318101536.webm]]

# ALU
Ahora que definimos una forma de hacer operaciones lógicas y aritméticas, podemos definir una Unidad Lógica Aritmética, un componente "caja negra", que recibe dos señales de números A y B de k bits, y una señal de selección S de 3 bits, que permite elegir qué operación (de 8: suma, resta, and, or, not, xor, shl, shr) realizar sobre los números entregados, y un output de k bits que entrega el resultado de la operación seleccionada.

## Circuitos de control
Para el correcto funcionamiento de una ALU se necesitan ciertos componentes base:
- Enabler
- Multiplexor: permite elegir un output entre dos inputs A y B con una señal S
- 