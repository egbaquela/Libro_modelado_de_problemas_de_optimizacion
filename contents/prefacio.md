# Prefacio {#sec:prefacio}

Este libro trata sobre el modelado, la resolución y el análisis de modelos de [Programación Lineal]() y derivados. No se focaliza en los algoritmos de resolución en si, sino mas bien en modelar correctamente el problema, resolverlo y analizar sus resultados. Es decir, apunta al practicante, no al teórico ni al diseñador de algoritmos. Si bien en algunos casos se necesitará programar algún algoritmo de resolución, el libro no se focaliza en como implementar el método [Simplex](), el [Branch and Bound]() y otros. Esta fuera del objetivo de este libro el tratamiento en profundidad de metaheurísticas y algoritmos de optimización mas avanzados, como el algoritmo de generación de columnas.

El público objetivo son estudiantes y graduados de Ingeniería Industrial e Ingeniería en Sistemas, por lo tanto, muchos de los ejemplos son específicos de estas disciplinas.

Si bien se utiliza el lenguaje de programación Julia, no es un libro sobre Julia, sino que se utiliza a modo de soporte en su resolución. Por eso, el contenido relativo a como instalar Julia y las bibliotecas necesarias se encuentra en los apéndices. Se puede usar el libro ignorando el código escrito en Julia (aunque claro, como los problemas se resuelven con dicho lenguaje, es necesario no saltarse las secciones para poder ver el análisis de las soluciones). Alternativamente, si solo queres aprender a modelar en Julia, con ver la descripción del problema ya podes ir directo al código.

El libro está estructurado siguiendo una lógica de familias de problemas, es decir, problemas que se modelan en forma similar. Ocasionalmente, se vuelve a una familia de problemas para agregarle complejidad o estudiar algoritmos mas complejos.

_Nota: este libro se creo utilizando el paquete [Books.jl](https://books.huijzer.xyz) del lenguaje de programación Julia [@bezanson2017julia] y la utilidad [pandoc](https://github.com/jgm/pandoc)._
