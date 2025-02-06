# Introducción {#sec:introduccion}

## ¿Que es un problema de optimización?
_Optimización_, _programación lineal_, _metaheurísticas_, términos que quizás metan un poco de miedo. O desconcierto. Pero, fuera de la jerga técnica, lo que hacemos cuando modelamos y resolvemos un problema de optimización no es nada mas analizar y sugerir que decisión tomar. Por ejemplo, dado un monto de dinero semanal para gastar en alimentos, que debería comprar para obtener el mejor beneficio nutricional. O, quizás, dados unos condicionantes nutricionales (no consumir mas de cierto porcentaje de grasas, por ejemplo), que debo comprar para gastar la menor cantidad de dinero posible. O, si manejo un camión de reparto y tengo que visitar a 10 clientes, ¿cual es la forma mas rápida de visitarlos?

Un problema de optimización se puede conceptualizar de la siguiente manera. Tenemos una decisión a tomar, la cual consiste en seleccionar una alternativa entre muchas (quizás infinitas). Queremos seleccionar la alternativa que sea mejor que el resto, para lo cual tenemos que tener una forma de compararlas (por ejemplo, el costo de la alternativa, el beneficio, la duración, etc, dependiendo de en que consista la decisión). Pero, además, tenemos que cumplir, obligatoriamente, ciertos criterios en la selección de alternativas. Veamos esto para los tres ejemplos anteriores:

* Dado un monto de dinero semanal para gastar en alimentos, que debería comprar para obtener el mejor beneficio nutricional: las alternativas aquí son todas combinaciones de alimentos disponibles. La forma de comparar las alternativas es midiendo su beneficio nutricional. El criterio obligatorio a cumplir es el de no gastar mas que el dinero disponible.

*  Dados unos condicionantes nutricionales (no consumir mas de cierto porcentaje de grasas), que debo comprar para gastar la menor cantidad de dinero posible: las alternativas aquí son todas combinaciones de alimentos disponibles. La forma de comparar las alternativas es mediante el costo total de la compra. Los criterios a cumplir son las cantidades mínimas y/o máximas de cada nutriente.

*  Si manejo un camión de reparto y tengo que visitar a 10 clientes, ¿cual es la forma mas rápida de visitarlos?: las alternativas son todas las secuencias en las cuales se pueden visitar los diez clientes. Por ejemplo, si les asigno números del 1 al 10, una alternativa es $[1,2,3,4,5,6,7,8,9,10]$, que significa visitar primero al cliente 1, luego al 2, luego al 3 y así sucesivamente hasta llegar al 10. Otra alternativa es $[10,9,8,7,6,1,2,3,4,5]$ es visitar primero al cliente 10, luego seguir con el 9, el 8, el 7, el 6, el 1, el 2, el 3, el 4 y, finalmente, el 5. El criterio usado para comparar alternativas es el tiempo de viaje. Los criterios obligatorios serían, entre otros, no excederse del horario de trabajo, visitar siempre a todos los clientes, no visitar a ningún cliente mas de una vez, etc.

Si bien las particulares de un problema de optimización depende en si de la situación que se intenta resolver, todos los problemas de optimización comparten esta estructura.

Los problemas de optimización aparecen por doquier, y de muchas maneras diferentes, en la vida diaria de las organizaciones. A veces sus componentes son fácilmente identificables, otras veces no. A veces, la información necesaria para armar el modelo de optimización se conoce con certeza, pero a veces (la mayoría de las veces) hay mucha incertidumbre. Algunas decisiones se toman una sola vez, otras se repiten rutinariamente todos los días. Si bien siempre apuntamos a alcanzar la mejor solución posible, en muchos nos casos nos conformamos con buenas soluciones cuando el costo y/o el tiempo necesarios para calcularla son prohibitivos.

## Modelado matemático de un problema de optimización
Los problemas de optimización, independientemente de su naturaleza, pueden modelarse mediante haciendonós las siguientes preguntas:

* ¿Cual es la meta a lograr?
* ¿Que factores puedo controlar para lograr esa meta?
* ¿Que factores no puedo controlar pero definen _cuanta meta_ consigo?
* ¿Que factores no puedo controlar pero restringen la forma en que puedo gestionar los factores controlables?

Apliquémoslo al siguiente problema:

> Tengo un taller que produce mesas y sillas. Hay mucha demanda, así que todo lo que fabrico se vende. Cada mesa fabricada (y vendida) me proporciona una beneficio de \$10 y cada silla de \$8. Fabricar una mesa requiere de 1 tablon grande y 4 tablones chicos. Fabricar una silla de 2 tablones grandes y 2 tablones chicos. Tengo 20 tablones de cada tipo. ¿Que debería fabricar para tener el mayor beneficio económico posible?

¿Cual es la meta a lograr?, bueno, acá es bastante sencillo, tener el mayor beneficio posible. Fijemosno que no queremos un buen beneficio, un beneficio aceptable, o un gran beneficio. Queremos el mayor beneficio posible. Es decir, nuestra meta es _maximizar el beneficio_, asegurarnos que no existe otra forma de producir mesas y sillas dados los recursos de los que disponemos que permita tener un beneficio mayor.

¿Que factores puedo controlar? En el ámbito del problema, es decir, de su narrativa, solo tengo poder de decisión en la cantidad de mesas y sillas a fabricar. No puedo modificar otra cosa. Ni los beneficios que me genera cada producto, ni los productos que ofrezco, ni la cantidad de tablones por producto ni la cantidad de tablones disponibles.

¿Que factores no puedo controlar pero definen _cuanta meta_ consigo? En este caso, los beneficios. No puedo controlarlos, es decir, no puedo modificarlos. Pero ciertamente, terminan definiendo el beneficio total que obtengo. ¿Que es el beneficio total?, la suma del beneficio de cada mesa multiplicado por la cantidad de mesas que fabrico mas el beneficio de cada silla multiplicado por la cantidad de sillas que fabrico. Solo puedo decidir sobre las cantidades a fabricar, pero los beneficios son la otra mitad de la ecuación.

¿Que factores no puedo controlar pero me limitan? En este caso, dos tipos de factores. La cantidad de tablones chicos y grandes que necesita cada silla y cada mesa (esto es, una tasa de consumo de tablones por unidad de producto), y la cantidad de tablones disponibles para consumir. ¿Y por que me limitan?, bueno, si tengo 20 tablones chicos, puedo fabricar cualquier cantidad de mesas y sillas siempre y cuando no consuma mas de 20 tablones chicos. Y lo mismo aplica a los grandes. Es decir, el consumo de recursos no puede ser mayor a la disponibilidad de recursos. 

Matematicemos esto. Puedo controlar, es decir, puedo decidir sobre, la cantidad de mesas y la cantidad de sillas que fabrico. Es mas, quiero saber cuanto fabricar de cada uno. Es decir, estas son las incognitas de mi problema. En términos de problemas de optimización, le damos el nombre de _variables de decisión_. Y como son incognitas, vamos a representarlas, en este caso, con la letra $x$. Tengo, entonces, dos _variables de decisión_:

* $x_{mesa}$, la cual representa la cantidad (por ahora desconocida) de mesas a fabricar.
* $x_{silla}$, la cual representa la cantidad (por ahora también desconocida) de silals a fabricar.

(notemos el detalle que en vez de llamar a una variable $cantidadDeMesas$ y a otra $cantidadDeSillas$, usamos la letra $x$ con un subíndice, $mesa$ y $silla$).

Con estas dos variables, es fácil representar mediante una ecuación el beneficio total. Si llamamos $Z$ al beneficio total, tenemos que:

* $Z = 10x_{mesa} + 8x_{silla}$

Si, por ejemplo, elejimos fabricar una mesa y dos sillas, el $x_{mesa}$ tomaría el valor $1$ y $x_{silla}$ el valor $2$. Por lo cual, $Z$ sería igual a:

* $Z = 10 \cdot 1 + 8 \cdot 2 = 26$

Recordemos que nuestra meta es la de maximizar el beneficio total. Esto lo podemos escribir como:

* Max $Z = 10x_{mesa} + 8x_{silla}$

Ahora bien, sería interesante fabricar $10000$ mesas y $25000$ sillas, pero no puedo. Estoy restringido por mis recursos. Dijimos antes que no puedo consumir mas recursos que los que tengo disponibles. Tanto la disponibilidad de tablones chicos como la cantidad de tablones chicos que necesita cada unidad (es decir, el consumo unitario) me ponen un límite a la cantidad de mesas y sillas a fábricar. Lo mismo pasa con los tablones grandes. La _restricción_ de los tablones chicos podemos escribirl de la siguiente manera:

* $1x_{mesa} + 2x_{silla} \leq 20$

En la inecuación anterior estamos diciendo que el consumo de tablones chicos (1 por cada mesa que fabrique y 2 por cada silla que fabrique) tiene que ser menor o igual a la disponibilidad de tablones chicos. De manera similar, podemos escribir la restricción de los tablones grandes:

* $4x_{mesa} + 2x_{silla} \leq 20$

Donde de nuevo decimos que el consumo de los tablones grandes debe ser menor a su disponibilidad.

Por último, es necesario acotar el rango de variación de las variables. Olvidándonos por un momento de las dos restricciones anteriores, las variables (la cantidad fabricada de mesas y sillas) podría tomar como valor cualquier número positivo (asumamos por ahora que podrían tomar valores con parte decimal). También podrían valer cero (no se produce el producto en cuestión). Pero no podrían tomar valores negativos. Esto lo podemos expresar como:

* $x_{mesa} \geq 0$
* $x_{silla} \geq 0$

