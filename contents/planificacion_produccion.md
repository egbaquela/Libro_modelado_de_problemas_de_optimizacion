# Planificación de la producción {#sec:planificacion_produccion}

## ¿Que es una problema de planificación de la producción?
Un problema de planificación de la producción es quizás el tipo de problemas mas sencillo de entender, sobre todo porque el modelado es bastante directo respecto de la narración del problema. En este tipo de problemas, hay que decidir cuanto producir de determinados bienes o servicios con el fin de tratar de maximizar el beneficio asociado a dicha producción. Ahora bien, para producir los bienes necesitamos consumir recursos. Cada producto tiene asociada una tasa de consumo de recursos y, a su vez, tenemos disponible una determinada cantidad de recursos. Por lo tanto, hay que obtener el mayor beneficio posible dado los recursos disponibles (es decir, no podemos consumir mas recursos que los que disponemos).

## Problema
Pensemos en el siguiente problema[^origen_winco]:

> Winco vende cuatro tipos de productos. Para satisfacer las demandas de los clientes, hay que producir exactamente $950$ unidades en total y por lo menos $400$ unidades del producto 4.
>
> En la tabla a continuación se dan los recursos requeridos para producir una unidad de cada producto y los precios de venta de cada uno. 
>
> |            Concepto         |    Producto 1     |    Producto 2     |    Producto 3     |    Producto 4     |
> |-----------------------------|-------------------|-------------------|-------------------|-------------------|
> | Materia Prima               | 2                 | 3                 | 4                 | 7                 |
> | Horas de trabajo            | 3                 | 4                 | 5                 | 6                 |
> | Precio de venta             | 4                 | 6                 | 7                 | 8                 |
>
>
> En la actualidad, se dispone de $4600$ unidades de materia prima y $5000$ horas de trabajo. 
>
> El objetivo de Winco es maximizar sus ingresos por las ventas. 

### Objetivos y variable de decisión
La detección de las variables de decisión y el objetivo del problema, suelen ir de la mano en muchos poblemas. Si leemos el enunciado del problema, dice explicitamente que Winco quiere maximizar sus ganancias, así que el objetivo debería ser ese. Y por otro lado, la única decisión que puede tomar Winco es acerca de cuanto producir de cada artículo. No puede elegir cambiar la cantidad de materia prima disponible, ni las horas de trabajo disponible, ni los estándares de trabajo (ya sea de horas o de materia prima) ni los precios de venta. 

Como solo se puede decidir acerca de la cantidad a producir de cada artículo, definamos estas magnitudes como variables de decisión:

$x_{i} \in \mathbb{R}, \ con \ i \in \{1,2,3,4\}$

Es decir, tenemos 4 variables de decisión reales, $x_{1}$, $x_{2}$, $x_{3}$ y $x_{4}$ (genericamente, $x_{i}$). Notemos que la notación $x_{i}$ me permitiría reutilizar la formulación con cualquier número de producto. En dicho caso, $i$ es una referencia al producto apuntado. 

Cualquier conjunto de valores de nuestras variables de decisión define a una solución potencial. Como, por ejemplo, $x_{1}=0$, $x_{2}=10$, $x_{3}=306.7632$ y $x_{4}=-3$. En forma mas compacta, $\vec{x}=(0, 10, 306.7632, -3)$. Que esta solución sea válida o no (factible, en términos de problemas de programación lineal) es otro cantar. 

¿Como podemos expresar el ingreso por ventas que obtendriamos para una solución potencial determinada? Bueno, en este problema, el ingreso por ventas se determina multiplicando el precio unitario de venta por la cantidad producida de un determinado artículo (se supone que la demanda absorbe la producción). O sea, para calcular el ingreso asociado al producto 1, tenemos que multiplicar $4$ por la cantidad producida, es decir, $x_{i}$. Repitiendo el mismo cálculo para cada producto y sumando los resultados, obtenemos nuestro ingreso por ventas, el cual es el objetivo a maximizar. Si denominamos $p_{i}$ al precio del artículo $i$:

Max $Z=\sum_{i=1}^{4}p_{i}x_{i}$

O, en forma extensa:

Max $Z=p_{1}*x_{1} + p_{2}*x_{2} + p_{3}*x_{3} + p_{4}*x_{4}$

O, expresando los valores de $p_{i}$:

Max $Z=4x_{1} + 6x_{2} + 7x_{3} + 8x_{4}$

Las tres formas de escribir la función $Z$ son equivalente para este problema. Pero la primera es mucho mas compacta. Y, las dos primeras, son reutilizables en un problema del mismo tipo pero con diferentes valores de precio unitario de venta.

### Restricciones
En la sección anterior dijimos que cualquier conjunto de valores para nuestras $x_{i}$ es una solución potencial, pero no todas las soluciones potenciales son factibles. En este problema, debo cumplir con la cantidad de $950$ unidades fabricadas en total, un mínimo de $400$ unidades del producto 4, no gastar mas materia prima de la disponible, ni mas horas de trabajo de las disponibles. Todo ello se expresa mediente las ecuaciones e inecuaciones que componen el conjunto de restricciones del problema.

La primer restricción me dice que que tengo que fabricar en total $950$ unidades. Es decir, la cantidad de productos $1$, $2$, $3$ y $4$ sumadas debe dar $950$. En forma de ecuación, si llamamos a la demanda total $DT$:

$\sum_{i=1}^{4}x_{i}=DT$

O, en forma extensa:

$x_{1} + x_{2} + x_{3} + x_{4} = 950$

Por otro lado, debo fabricar como mínimo $400$ unidades del artículo $4$. Si llamamos a esta cantidad $DMin_{4}$:

$x_{4} \geq DMin_{4}$

O en forma extensa (o explícita):

$x_{4} \geq 400$

Por otro lado, no tengo que consumir mas materia prima que la disponible. Si llamo $m_{i}$ a la cantidad de materia prima que necesita una unidad del producto $i$, y $MP$ a la cantidad de materia prima total:

$\sum_{i=1}^{4}m_{i}x_{i} \leq MP$

O, en forma mas extensa:

$2x_{1} + 3x_{2} + 4x_{3} + 7x_{4} \leq 4600$

Por el lado de las horas disponibles, la formulación es similar al caso de la materia prima. Si llamamos $h_{i}$ a la cantidad de horas de trabajo que necesita una unidad del producto $i$ y $HT$ a la cantidad de horas de trabajo totales:

$\sum_{i=1}^{4}h_{i}x_{i} \leq HT$

O, en forma mas extensa:

$3x_{1} + 4x_{2} + 5x_{3} + 6x_{4} \leq 5000$

Por último, ninguna variable de decisión puede tomar valores negativos:

$x_{i}\geq 0$

O en forma extensa:

$x_{1}\geq 0$
$x_{2}\geq 0$
$x_{3}\geq 0$
$x_{4}\geq 0$

### Formulación completa
El problema completo en forma compacta (en realidad, podría ser mas compacto todavía) es:

$Max \ Z=\sum_{i=1}^{4}p_{i}x_{i}$

Sujeto a:

$\sum_{i=1}^{4}x_{i}=DT$

$x_{4} \geq DMin_{4}$

$\sum_{i=1}^{4}m_{i}x_{i} \leq MP$

$\sum_{i=1}^{4}h_{i}x_{i} \leq HT$

$x_{i}\geq 0$

En forma extensa (o explícita):

$Max \ Z=4x_{1} + 6x_{2} + 7x_{3} + 8x_{4}$

Sujeto a:

$x_{1} + x_{2} + x_{3} + x_{4} = 950$

$x_{4} \geq 400$

$2x_{1} + 3x_{2} + 4x_{3} + 7x_{4} \leq 4600$

$3x_{1} + 4x_{2} + 5x_{3} + 6x_{4} \leq 5000$

$x_{1}\geq 0$
$x_{2}\geq 0$
$x_{3}\geq 0$
$x_{4}\geq 0$

La forma compacta nos permite establecer una familia de problemas, mientras que la forma extensa nos permite especificar un problema puntual. Fijémosnos que, cualesquiera sean los valores que tomen $DT$, $Dmin_{4}$, $p_{i}$, $h_{i}$ y $m_{i}$, la forma compacta es todavía válida.

### Modelado y resolución con Julia

```jl
code = """
    using HiGHS, JuMP;
    """
sc(code)
```

```jl
using HiGHS, JuMP
code = """
    # Modelo vacío
    model_v2 = Model(HiGHS.Optimizer);

    # Parámetros del modelo
    c_v2 = [4;6;7;8];
    a1_v2 = [1;1;1;1];
    a3and4_v2 = [
        2 3 4 7
        3 4 5 6];
    b3and4_v2 = [4600; 5000];

    # Variables
    x_v2 = @variable(model_v2, x_v2[1:4] >= 0);

    # Función objetivo
    obj_v2 = @objective(model_v2, Max, 
        sum([c_v2[i] * x_v2[i] for i in 1:4]));

    # Restricciones
    r1_v2 = @constraint(model_v2, 
        sum([a1_v2[i] * x_v2[i] for i in 1:4]) == 950);

    r2_v2= @constraint(model_v2, x_v2[4] >= 400);

    r3and4_v2 = @constraint(model_v2, 
        [j in 1:2], #Genero dos restricciones
        sum([a3and4_v2[j,i] * x_v2[i] for i in 1:4 ]) <= b3and4_v2[j]);

    """
sc(code)
```

Podemos ver el modelo generado por el código anterior mediante la función Text, la cual arroja la siguiente salida:

```jl
code = """
    Text(model_v2)
    """
sco(code)
```

Listo, tenemos el modelo, vamos a resolverlo:


```jl
code = """
    optimize!(model_v2)
    """
sc(code)
```

Inspeccionemos el resultado:

```jl
code = """
    solution_summary(model_v2)
    """
sco(code)
```

Genial, vemos que dice que `Termination status : OPTIMAL`. Esto significa que el _solver_ pudo encontrar la solución óptima del problema. El _summary_ no da mas información sobre la solución, pero implica leer todo el reporte. Podemos inspeccionar cada parte con algunas funciones dedicadas:

```jl
code = """
    termination_status(model_v2)
    """
sco(code)
```

Vemos que nos dice que la solución es óptima. ¿Cual es el valor de la función objetivo?

```jl
code = """
    objective_value(model_v2)
    """
sco(code)
```

[^origen_winco]: Desde hace varios años vengo utilizando este problema en mis clases como disparador, pero no pude encontrar la referencia bibliográfica. Tenía la impresión que lo había extraido del Hillier, pero no, no lo encontré ahí. Si alguien puede pasarme la referencia, se los agradezco.
