# Introducción {#sec:introduccion}
En esta sección veremos ejemplos de uso de modelado matemático para problemas de optimización. Discutiremos acerca de los usos y aplicaciones. Al finalizar, se presentará la estructura general del libro.

## ¿Que es un problema de optimización?
_Optimización_, _programación lineal_, _metaheurísticas_, términos que quizás metan un poco de miedo. O desconcierto. Pero, fuera de la jerga técnica, lo que hacemos cuando modelamos y resolvemos un problema de optimización no es nada mas analizar y sugerir que decisión tomar. Por ejemplo, dado un monto de dinero semanal para gastar en alimentos, que debería comprar para obtener el mejor beneficio nutricional. O, quizás, dados unos condicionantes nutricionales (no consumir mas de cierto porcentaje de grasas, por ejemplo), que debo comprar para gastar la menor cantidad de dinero posible. O, si manejo un camión de reparto y tengo que visitar a 10 clientes, ¿cual es la forma mas rápida de visitarlos?

Un problema de optimización se puede conceptualizar de la siguiente manera. Tenemos una decisión a tomar, la cual consiste en seleccionar una alternativa entre muchas (quizás infinitas). Queremos seleccionar la alternativa que sea mejor que el resto, para lo cual tenemos que tener una forma de compararlas (por ejemplo, el costo de la alternativa, el beneficio, la duración, etc, dependiendo de en que consista la decisión). Pero, además, tenemos que cumplir, obligatoriamente, ciertos criterios en la selección de alternativas. Veamos esto para los tres ejemplos anteriores:

* Dado un monto de dinero semanal para gastar en alimentos, que debería comprar para obtener el mejor beneficio nutricional: las alternativas aquí son todas combinaciones de alimentos disponibles. La forma de comparar las alternativas es midiendo su beneficio nutricional. El criterio obligatorio a cumplir es el de no gastar mas que el dinero disponible.

*  Dados unos condicionantes nutricionales (no consumir mas de cierto porcentaje de grasas), que debo comprar para gastar la menor cantidad de dinero posible: las alternativas aquí son todas combinaciones de alimentos disponibles. La forma de comparar las alternativas es mediante el costo total de la compra. Los criterios a cumplir son las cantidades mínimas y/o máximas de cada nutriente.

*  Si manejo un camión de reparto y tengo que visitar a 10 clientes, ¿cual es la forma mas rápida de visitarlos?: las alternativas son todas las secuencias en las cuales se pueden visitar los diez clientes. Por ejemplo, si les asigno números del 1 al 10, una alternativa es $[1,2,3,4,5,6,7,8,9,10]$, que significa visitar primero al cliente 1, luego al 2, luego al 3 y así sucesivamente hasta llegar al 10. Otra alternativa es $[10,9,8,7,6,1,2,3,4,5]$ es visitar primero al cliente 10, luego seguir con el 9, el 8, el 7, el 6, el 1, el 2, el 3, el 4 y, finalmente, el 5. El criterio usado para comparar alternativas es el tiempo de viaje. Los criterios obligatorios serían, entre otros, no excederse del horario de trabajo, visitar siempre a todos los clientes, no visitar a ningún cliente mas de una vez, etc.

Si bien las particulares de un problema de optimización depende en si de la situación que se intenta resolver, todos los problemas de optimización comparten esta estructura.

Los problemas de optimización aparecen por doquier, y de muchas maneras diferentes, en la vida diaria de las organizaciones. A veces sus componentes son fácilmente identificables, otras veces no. A veces, la información necesaria para armar el modelo de optimización se conoce con certeza, pero a veces (la mayoría de las veces) hay mucha incertidumbre. Algunas decisiones se toman una sola vez, otras se repiten rutinariamente todos los días. Si bien siempre apuntamos a alcanzar la mejor solución posible, en muchos nos casos nos conformamos con buenas soluciones cuando el costo y/o el tiempo necesarios para calcularla son prohibitivos.




## ¿Como sigue este libro?
A partir del siguiente capítulo, el libro se enfocará en tratar familias de problemas, presentando herramientas adicionales y/o metodologías de modelado a medida que los problemas lo requieran. El enfoque será el de presentar la narrativa del problema, discutir acerca de su modelado matemático, luego presentar la implementación en _Julia_ y el análisis de los resultados. 