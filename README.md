# Modelado y resolución de problemas de optimización
 Repositorio del libro, con la versión actualizada del código y cada una de las releases.


## ¿Como compilar el libro?
Aquellos que quieran construir el libro desde el código, pueden hacerlo de la siguiente manera. Es necesario que instalen el paquete previamente el _[Books.jl](https://github.com/JuliaBooks/Books.jl)_, mediante:

```
julia>using Pkg
julia>Pkg.add("Books")
```

La mejor forma de trabajar es abrir dos terminales en paralelo. En una terminal ejecutar:
```
julia --project -e 'using Books; serve()'
```

Esto arranca un servidor que ejecuta el libro en formato web. A medida que vayamos modificando los archivos del proyecto, el libro se actualizará en tiempo real (luego de guardar los cambios, obvio). 

Si agregamos nuevo código de _Julia_, o bien queremos generar el PDF, necesitamos la otra terminal:

```
julia --project -ie 'using Books'
julia>gen() # Cada vez que agreguemos código en Julia que queremos que se ejecute, como un modelo JuMP por ejemplo.
julia>pdf() # Cuando queramos generar el PDF
```

Para mas información acerca de las opciones de _Books.jl_, ver [https://huijzer.xyz/Books.jl/](https://huijzer.xyz/Books.jl/)

## ¿Como citar el libro?
Si vas a usar el libro en tus clases, para un artículo académico, o para cualquier otro material, por favor citalo de la siguiente manera:

> Baquela, E. G. (2025), Modelado y resolución de problemas de optimización. Recuperado de https://github.com/egbaquela/libro_optimizacion

En formato BIBTEX:

> @book{baquela2025librooptimizacion,
>   title = {Modelado y resolución de problemas de optimización},
>   author = {Enrique Gabriel Baquela},
>   url = {https://github.com/egbaquela/libro_optimizacion},
>   year = {2025}
> }

