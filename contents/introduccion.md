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

Esta es la _función objetivo_ de nuestro problema. Recordemos que nuestra meta es la de maximizar el beneficio total. Esto lo podemos escribir como:

* Max $Z = 10x_{mesa} + 8x_{silla}$

Ahora bien, sería interesante fabricar $10000$ mesas y $25000$ sillas, pero no puedo. Estoy restringido por mis recursos. Dijimos antes que no puedo consumir mas recursos que los que tengo disponibles. Tanto la disponibilidad de tablones chicos como la cantidad de tablones chicos que necesita cada unidad (es decir, el consumo unitario) me ponen un límite a la cantidad de mesas y sillas a fábricar. Lo mismo pasa con los tablones grandes. La _restricción_ de los tablones chicos podemos escribirl de la siguiente manera:

* $x_{mesa} + 2x_{silla} \leq 20$

En la inecuación anterior estamos diciendo que el consumo de tablones chicos (1 por cada mesa que fabrique y 2 por cada silla que fabrique) tiene que ser menor o igual a la disponibilidad de tablones chicos. De manera similar, podemos escribir la restricción de los tablones grandes:

* $4x_{mesa} + 2x_{silla} \leq 20$

Donde de nuevo decimos que el consumo de los tablones grandes debe ser menor a su disponibilidad.

Por último, es necesario acotar el rango de variación de las variables. Olvidándonos por un momento de las dos restricciones anteriores, las variables (la cantidad fabricada de mesas y sillas) podría tomar como valor cualquier número positivo (asumamos por ahora que podrían tomar valores con parte decimal). También podrían valer cero (no se produce el producto en cuestión). Pero no podrían tomar valores negativos. Esto lo podemos expresar como:

* $x_{mesa} \geq 0$
* $x_{silla} \geq 0$

Y así, tenemos nuestro modelo matemático armado. Poniendo todo junto:

> Max $Z = 10x_{mesa} + 8x_{silla}$
>
> Sujeto a:
>
> &emsp; $x_{mesa} + 2x_{silla} \leq 20$
>
> &emsp; $4x_{mesa} + 2x_{silla} \leq 20$
>
> &emsp; $x_{mesa} \geq 0$
>
> &emsp; $x_{silla} \geq 0$

Y listo, nuestra narrativa original del problema está expresada en un modelo matemático equivalente. Cualquier par de valores $(x_{mesa},x_{silla})$ es una solución de este problema. Por ejemplo, $x_{mesa}=1$ y $x_{silla}=0$, o escrito en forma vectorial, $(1;0)$. $(-1;0)$, $(2,1)$, $(5, 50000)$ todas son soluciones, pero no todas son soluciones del mismo tipo. Para empezar, $(-1;0)$ y $(5, 50000)$ son soluciones que violan las restricciones (la primera viola la restricción que $x_{mesa}$ no puede ser negativa, la segunda viola las dos restricciones de consumos de recursos). Estas soluciones que hacen que al menos una restricción no se cumple, se denominan _soluciones infactibles_. La violación de las restricciones la podemos constatar reemplazando $x_{mesa}$ y $x_{silla}$ por los valores propuestos. Por ejemplo, para la solución $x_{mesa}=-1$ y $x_{silla}=0$ vemos que la restricción $x_{mesa} \geq 0$ no se cumple, ya que si reemplazo $x_{mesa}$ por $-1$, tengo:

* $-1 \geq 0$

Lo cual es falso.

Por otro lado, soluciones como $(1;0)$ y $(2,1)$ son soluciones que no violan ninguna restricción. Por ejemplo, para la segunda, si reemplazo los valores de $x_{mesa}$ y $x_{silla}$ obtengo:

* $2 + 2 \cdot 1 \leq 20$ -> $4 \leq 20$
* $4x \cdot 2 + 2 \cdot 1 \leq 20$ -> $10 \leq 20$
* $2 \geq 0$
* $1 \geq 0$

Este tipo de soluciones, que no violan ninguna restricción, se denominan _soluciones factibles_. Factibles porque, en este caso del plan de producción, puedo llevar ese plan a la práctica; es decir, puede realmente producir 2 mesas y 1 silla dados los recursos disponibles. Ahora bien, tanto $(1;0)$ y $(2,1)$ son factibles, pero podemos ver que la segunda es mejor que la primera. Si reemplazamos los valores de $x_{mesa}$ y $x_{silla}$ en la función objetivo tenemos, para la primera y la segunda solución respectivamente:

*  $Z = 10 \cdot 1 + 8 \cdot 0 = 10$
*  $Z = 10 \cdot 2 + 8 \cdot 1 = 28$

Es decir, las dos soluciones son factibles, pero de las dos, la segunda es mejor que la primera. Ahora bien, hay mas soluciones factibles que estás dos que dimos de ejemplo. De hecho, como por ahora estamos permitiendo tener valores fraccionarios, como $(2,5; 3,23558)$, en realidad hay infinitas soluciones posibles. Y, obviamente, revisar y comparar infinitas soluciones nos tomaría un tiempo infinito. Si, no parece muy buena idea la de inspeccionar todas las soluciones. Pero para ello, podemos hacer uso de los _algoritmos de resolución_ de problemas de optimización. 


## Instalación y configuración de las herramientas de resolución
Bueno, ok, _Julia time_. En realidad, _solver time_. Para poder resolver nuestro problema de optimización, es decir, encontrar los mejores valores de $x_{mesa}$ y $x_{silla}$ (es decir, determinar nuestro plan de producción), es necesario ayudarnos con algún software que implemente un algoritmo de resolución acorde al problema modelado. En nuestro caso, un _algoritmo de resolución de problemas de programación lineal_. Genericamente, los softwares (o bibliotecas para lenguajes de programación, o plugin para planillas de cálculo, etc) se denominan _solvers_. Estos _solvers_ son los encargados de resolver las ecuaciones y proporcionar una solución para nuestros problemas. Adicionalmente, existe otra categoría de softwares, los softwares de _modelado_ que nos permiten modelar el problema en una computadora en forma similar como escribimos las ecuaciones de un problema, y enviar dicho modelo a un _solver_. Es decir, la herramienta de _modelado_ no resuelve, pero nos ayuda a llamar al _solver_ de una manera mas amistosa (para nosotros).

¿Que herramientas vamos a utilizar aquí? Vamos a utlizar el lenguaje de programación _Julia_, la biblioteca de _modelado_ _JuMP_, y el _solver_ _HiGHS_. En los archivos adicionales compartidos con el libro, todos estos modelos van a estar implementados en un _notebook_ de _Pluto_. _Julia_ es un lenguaje de programación multi-propósito pero fuertemente orientado a las aplicaciones científicas. _JuMP_ es una biblioteca de modelado algebraico que permite modelar, entre otros, problemas de programación lineal (que sería el tipo de problema de nuestro ejemplo de metas y sillas). Es muy práctico porque tiene una sintaxis muy similar a la formulación matemática del problema, por lo cual es casi, casi, como escribirlo en papel y lápiz. Y HiGHS es un _solver_ programado principalemnte en _C++_ pero con interfaces para varios lenguajes de programación, entre ellos _Julia_. Las tres herramientas mencionadas son Open Source y tienen una amplia comunidad de usuarios.

¿Como instalar y ejecutar _Julia_ y el resto de las herramientas? Hagamos un parate con la resolución del problema y vayamos paso a paso con la instalación.

Para instalar _Julia_, primero hay que descargarlo. El sitio web oficial de _Julia_ es [https://julialang.org/](https://julialang.org/), y mediante el se puede acceder a la página de descargas: https://julialang.org/downloads/](https://julialang.org/downloads/). Desde la página de descargas, tenemos varias opciones para gestionar la instalación, pero lo mejor es instalar _juliaup_, un gestor de versiones de _Julia_ que nos va a facilitar la posterior actualización del sistema, a medida que nuevas versiones sean lanzadas. Si estamos en _Linux_, en una terminal escribimos el siguiente comando (tal cual lo indica la web):

```
curl -fsSL https://install.julialang.org | sh
```

Si estamos en _Windows_, abrimos la aplicación _CMD_ (también llamado _Símbolo del Sistema_, pero tipeando CMD en la barra de búsqueda se encuentra mas rápido; si esto te suena extraño, leete el apéndice _Julia en Windows_ ) e ingresamos el siguiente comando:

```
winget install julia -s msstore
```

Y esperamos un rato a que se instale. Cuando finalize, podemos ejecutar _Julia_ abriendo una terminal (en _Windows_, abriendo la _CMD_ abierta; de aquí en adelante utilizaremos el término mas general _terminal_) tipeando:

```
julia
```

Y deberíamos ver algo como lo siguiente:

![Imagen terminal Julia](/images/terminal_julia.png)

Una vez instalado, es necesario instalar las bibliotecas (paquetes en la terminología de _Julia_) que queremos utilizar. Por defecto, _Julia_ trae las herramientas mínimas para programar. Poderosas, si, pero mínimas. Funcionalidad adicional, en forma de tipos de datos y algoritmos prefabricados, se encapsulan en paquetes y se ponen a disposición en el repositorio general. Entre los mínimo con lo que _Julia_ viene de fábrica, está el gestor de paquetes, el _Pkg_. Con una terminal abierta, si hacemos:

```
using Pkg
```

cargamos el gestor de paquetes en memoria (esto es una constante, cada vez que queramos utilizar alguna funcionalidad no básica, hay que cargar el correspondiente paquete a meoria con el comando _using_ seguido del nombre de paquetes; cuidado que para _Julia_ las mayúsculas son diferentes que las minúsculas).

Con el gestor de paquetes en memoria, podemos instalar nuevos paquetes llamando a la función _add_ de _Pkg_ pasando el nombre del paquete como parámetro. Por ejemplo, para instalar el paquete _JuMP_ hacemos:

```
Pkg.add("JuMP")
```

Para asegurarnos de trabajar sin problemas con los modelos y ejercicios de este libro, vamos a instalar los siguientes paquetes:

* JuMP
* NamedArrays
* HiGHS
* DataFrames
* CSV
* XLSX
* Pluto
* PlutoUI

El proceso completo para instalarlos, incluyendo la carga a memoria de _Pkg_, es el siguiente:

```
using Pkg
Pkg.add("JuMP")
Pkg.add("NamedArrays")
Pkg.add("HiGHS")
Pkg.add("DataFrames")
Pkg.add("CSV")
Pkg.add("XLSX")
Pkg.add("Pluto")
Pkg.add("PlutoUI")
```

Listo, con esto ya tenemos nuestro entorno configurado para trabajar correctamente. Hay que tener en cuenta que, para trabajar mas fácilmente, siempre conviene ejecutar _Julia_ con la terminal abierta en el directorio o carpeta en el cual tenemos los archivos con los cuales vamos a trabajar (de nuevo, se puede consultar el apéndice _Julia en Windows_ para esto).

La modalidad de trabajo depende de las preferencias de cada uno. En los apéndice _Usando Julia desde la terminal_, _Usando Julia mediante scripts_ y _Usando Julia con Pluto_ tenemos tres formas diferentes de utilizar _Julia_ para modelar problemas de optimización. El modelado en la terminal es ciertamente inconveniente, las otras dos maneras son mas amistosas, siendo, a mi parecer, usar _Pluto_ la mejor opción para analisís puntuales. El apéndice _Usando Julia mediante Google Colab_ muestra como ejecutar un script de en una máquina virtual en la nube.

Un comentario mas. _Julia_ es un lenguaje de programación con compilación en tiempo real (_JIT_, por _just in time_). Esto, desde nuestro punto de vista, se traduce en que la primera vez en cada sesión (es decir, para cada ejecución de _Julia_) que llamemos a una función, esta demora mas tiempo que las siguientes veces que la llamemos. Si la función en si necesita mucho tiempo para ejecutarse no vamos a notar la diferencia, pero para funciones que requieren poco tiempo, nos vamos a dar cuenta que la primera vez tarda un montón. 

## Resolución del problema de optimización
Listo. Modelamos el problema, instalamos _Julia_ y todos los paquetes relacionados. Ya podemos comenzar a traducir el modelo matemático al formato de _JuMP_ y obtener la solución. Recordemos que todo el código que desarrollemos lo podemos escribir en la terminal, en un archivo de texto (script) o en un notebook de Pluto o de Colab. En el material complementario de este libro, podemos encontrar el script y los notebooks correspondientes a esta resolución.

Bueno, comencemos con la resolución. Lo primero que debemos hacer, es importar los paquetes que necesitamos para el modelado:


```jl
code = """
    using HiGHS, JuMP, NamedArrays;
    """
sc(code)
```

Recordemos que si lo estamos ejecutando en _Pluto_, y no queremos descargar nuevamente los paquetes, hay que indicarle previamente a _Pluto_ que use el gestor de paquetes global de _Julia_, no su instancia particular (ver apendice _Usando Julia con Pluto_):

```
begin
	import Pkg;
	Pkg.activate();
end
```

Importando los paquetes, ya podemos crear un modelo vacío:

```jl
code = """
    model_intro_01 = Model(HiGHS.Optimizer)
    """
sco(code)
```

Lo que estamos haciendo aquí es crear un modelo vacío al cual guardamos en una variable llamada _model_intro_01_ y asociarle el _solver HiGHS_ para su posterior resolución. Con el modelo definido, ya podríamos crear las variables de decisión de nuestro modelo:


```jl
code = """
    @variable(model_intro_01, xmesa >= 0)
    """
sco(code)
```

Con la función (bueno, con la _macro_ en realidad) _\@variable_ le estamos indicando crear una variable, a la cual llamamos _xmesa_, y la declaramos como no-negativa (es decir, mayor o igual a cero). El primer parámetro pasado a _\@variable_ es el modelo al cual queremos agregar la variable, el segundo una expresión que al mismo tiempo declara la variable y le asocia la restricción de no-negatividad. Observen como cambia el modelo:


```jl
code = """
    model_intro_01
    """
sco(code)
```

Si, escribiendo el nombre de la variable que almacena el modelo, _Julia_ nos muestra un resumen del mismo. Creemos la varaible _xsilla_ ahora, y mostremos el resumen del modelo:

```jl
code = """
    @variable(model_intro_01, xsilla >= 0)
    model_intro_01
    """
sco(code)
```

Teniendo nuestra variables, podemos crear la función objetivo, usando para ellos _\@objective_. Sus parámetros son el modelo, el sentido del problema (_Max_ para maximizar, _Min_ para minimizar), y la expresión, la formula matemática, de la función objetivo:

```jl
code = """
    @objective(model_intro_01, Max,  10*xmesa + 8*xsilla)
    model_intro_01
    """
sco(code)
```

Fijémosnos la similitud con la escritura matemática de la función objetivo:

> Max $Z = 10x_{mesa} + 8x_{silla}$

Tenemos el _Max_, las variables, los coeficientes que los multiplican y la suma. La traducción a código es casi literal. Cremos las restricciones ahora, utilizando _\@constraint_. Vamos a crear todas las restricciones juntas (salvo las de no-negatividad, que ya las creamos). Los parámetros a pasar son el modelo, el nombre de la restricción (esto es opcional, podemos omitir este parámetro), y la formula matemática de la restricción:


```jl
code = """
    @constraint(model_intro_01, restriccion_tablones_chicos, xmesa + 2*xsilla <= 20) 
    @constraint(model_intro_01, restriccion_tablones_grandes, 4*xmesa + 2*xsilla <= 20)
    model_intro_01
    """
sco(code)
```

De nuevo, fijémosnos que similar es este código con la escritura matemática:

> &emsp; $x_{mesa} + 2x_{silla} \leq 20$
>
> &emsp; $4x_{mesa} + 2x_{silla} \leq 20$

Y listo, tenemos nuestro modelo creado. ¿Como podemos verificar realmente que las ecuaciones estén dentro del modelo?, bueno, podemos usar la función _Text_:

```jl
code = """
    Text(model_intro_01)
    """
sco(code)
```

La función _Text_ es muy útil, pero solo cuando el modelo es chico (es decir, pocas variables y pocas restricciones). Para modelos grandes, la cantidad de datos a mostrar es tan grande que se vuelve ilegible en la práctica.

Si, esta bien, tenemos el modelo, pero todavía no se cual es la mejor combinación de mesas y sillas. Llamemos entonces al _solver_ para que lo resuelva:

```jl
code = """
    optimize!(model_intro_01)
    termination_status(model_intro_01)
    """
sco(code)
```

La función _optimize!_ es la encargada de llamar al _solver_ asociado al modelo (_HiGHS_) en nuestro caso. Dependiendo de donde lo utilicemos, y del solver utilizado, podemos obtener como salidas intermedias de la función el log de los pasos realizados por el _solver_. La información relativa a la resolución se guarda dentro del mismo modelo. _termination_status_ devuelve cual es el estado del modelo luego de intentar su resolución; es este caso, se pudo encontrar la solución óptima. Ahora bien, ¿cuantas mesas tengo que fabricar?:

```jl
code = """
    value(model_intro_01[:xmesa])
    """
sco(code)
```

No hay que fabricar mesas. ¿Y sillas?:

```jl
code = """
    value(model_intro_01[:xsilla])
    """
sco(code)
```

Pero si sillas, $10$. Entonces, el mejor plan de producción es fabricar $10$ sillas y ninguna mesa, es decir, $(0;10)$. ¿Cual es el beneficio que obtenemos?:

```jl
code = """
    objective_value(model_intro_01)
    """
sco(code)
```

Obtengo en total un beneficio de $80$, el mayor beneficio posible dado los recursos disponibles. ¿Cuantos tablones chicos consumimos en total?:

```jl
code = """
    value(model_intro_01[:restriccion_tablones_chicos])
    """
sco(code)
```

¿Y cuantos tablones grandes?:


```jl
code = """
    value(model_intro_01[:restriccion_tablones_grandes])
    """
sco(code)
```

Es decir, consumimos todos los recursos disponibles para producir solo sillas, obteniendo de esto el máximo beneficio posible. Esta consulta acerca de cuantos recursos consumimos solo la podemos realizar, al menos en esta forma, si declaramos la restricción con nombre (el parámetro opcional de _\@constraint_).

Ahora bien, ¿no me convendría fabricar alguna mesa? Bueno, vemos. Para fabricar una única mesa, voy a necesitar $1$ tablón chico y $4$ tablones grandes. Estos tablones, dado que tengo una cantidad limitada, los voy a tener que dejar de fabricar algunas sillas. En términos de tablones chicos, una mesa es equivalente a media silla (la silla requiere el doble de estos tablones), pero en términos de tablones grandes, la mesa equivale a dos sillas. Es decir, para producir una mesa, debo dejar de producir dos sillas. La solución entonces sería $(1;8)$. El beneficio asociado sería:

> $10 \cdot 1 + 8 \cdot 8 = 74$

Lo cual vemos que es claramente menor al beneficio obtenido fabricando solamente sillas. Tampoco podemos fabricar mas de $10$ sillas, porque consumimos los $20$ tablones chicos y los $20$ tablones grandes disponibles.

## ¿Como sigue este libro?
A partir del siguiente capítulo, el libro se enfocará en tratar familias de problemas, presentando herramientas adicionales y/o metodologías de modelado a medida que los problemas lo requieran. El enfoque será el de presentar la narrativa del problema, discutir acerca de su modelado matemático, luego presentar la implementación en _Julia_ y el análisis de los resultados. 