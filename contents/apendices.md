# Apéndices {#sec:apendices}

## Julia en Windows {#sec:apendice_julia_en_windows}

## Usando Julia desde la terminal {#sec:apendice_julia_desde_terminal}

## Usando Julia mediante scripts {#sec:apendice_julia_con_scripts}

## Usando Julia con Pluto {#sec:apendice_julia_con_pluto}

## Usando Julia mediante Google Colab {#sec:apendice_julia_con_colab}

## Modelando problemas con Julia {#sec:modelado_con_julia}
Para resolver problemas de Programación Lineal con Julia, es necesario recurrir a algún paquetes (o biblioteca) que nos permita trasladar el formalismo de la PL en forma fácil y, a su vez, conectarnos a un solver. En este libro utilizamos la bilioteca de modelado [JuMP](https://jump.dev/) y el solver [HiGHS](https://www.maths.ed.ac.uk/hall/HiGHS/).

_JuMP_ es una biblioteca de modelado que permite escribir modelos de PL en Julia de forma muy similar a la escritura matemática estandar. En ese sentido, sabiendo como escribir las ecuaciones en papel y lápiz, es poco lo que se necesita aprender de Julia para resolver problemas de PL.

_HiGHS_ es un solver Open-Source desarrollado por un equipo de investigadores de la Universidad de Edimburgo. Dentro del grupo de los solvers no comerciales es, junto con SCIP, uno de los solvers mas potentes para resolver problemas de PL y PL Entera-Mixta. Si bien inferior en velocidad respecto de solvers como CPLEX y Gurobi, es adecuado para una gran cantidad de aplicaciones en la industria.

Para instalarlos, en una terminal de _julia_, tipeamos:

```
using Pkg;
Pkg.add("JuMP");
Pkg.add("HiGHS");
```

Luego, cuando necesitemos usarlos, los cargamos en memoria mediante:

```jl
code = """
    using HiGHS, JuMP;
    """
sc(code)
```

Supongamos que queremos modelar el siguiente problema:

> $\begin{equation}
> Min Z = 4x_{1} + 6x_{2} + 7x_{3} + 8x_{4} 
> \end{equation}$
> 
> Sujeto a:
> 
> $\begin{equation}
> x_{1} + x_{2} + x_{3} + x_{4} = 950
> \end{equation}$
> 
> $\begin{equation}
> x_{4} \geq 400
> \end{equation}$
> 
> $\begin{equation}
> 2x_{1} + 3x_{2} + 4x_{3} + 7x_{4} \leq 4600
> \end{equation}$
> 
> $\begin{equation}
> 3x_{1} + 4x_{2} + 5x_{3} + 6x_{4} \leq 5000
> \end{equation}$
> 
> $\begin{equation}
> x_{i} \geq 0,  \forall i \in \{1,2,3,4\}
> \end{equation}$

Una formulación casi textual sería

```jl
using HiGHS, JuMP
code = """
    model_v2 = Model(HiGHS.Optimizer)
    c_v2 = [4;6;7;8]
    a1_v2 = [1;1;1;1]
    a3and4_v2 = [
        2 3 4 7
        3 4 5 6]
    b3and4_v2 = [4600; 5000]

    x_v2 = @variable(model_v2, x_v2[1:4] >= 0)

    obj_v2 = @objective(model_v2, Max, 
        sum([c_v2[i] * x_v2[i] for i in 1:4]))

    r1_v2 = @constraint(model_v2, 
        sum([a1_v2[i] * x_v2[i] for i in 1:4]) == 950)

    r2_v2= @constraint(model_v2, x_v2[4] >= 400)

    r3and4_v2 = @constraint(model_v2, 
        [j in 1:2], #Genero dos restricciones
        sum([a3and4_v2[j,i] * x_v2[i] for i in 1:4 ]) <= b3and4_v2[j])

    Text(model_v2)

    """
sco(code)
```

`Text(model_v2)` es totalmente opcional, y no deberíamos ejecutarlo cuando el modelo es muy grande. Sirve a efectos de depuración cuando se está construyendo un modelo, en general con un conjunto de datos chico.

Para resolverlo:

```jl

code = """
    optimize!(model_v2)
    """
sco(code)
```

## Modelando problemas con Excel (u otra planilla de cálculo) {#sec:modelado_con_planilla_de_calculo}
