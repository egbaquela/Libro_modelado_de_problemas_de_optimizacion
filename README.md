# Example

Example book

See <https://booktemplate.huijzer.xyz/> for more information.

Book created with [https://github.com/JuliaBooks/Books.jl](Books.jl)

En una terminal ejecutar:
```
julia --project -e 'using Books; serve()'
```

En otro terminal:

```
julia --project -ie 'using Books'
julia>gen()
julia>pdf()
```

Cada vez que se genere el libro, habría que borrar el contenido de _gen. En caso contrario, el código no se genera. Luce como un error de la biblioteca. O quizás sucede cuando se genera algún error en el código.
