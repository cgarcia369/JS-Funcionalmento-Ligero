# JavaScript Funcionalmente-Ligero

<a href="https://leanpub.com/fljs"><img src="images/marketing/front-cover-small.png" width="20%"></a>

[![Buy on Leanpub](https://img.shields.io/badge/Buy-Leanpub-yellow.svg)](https://leanpub.com/fljs) [![Buy on Amazon](https://img.shields.io/badge/Buy-Amazon-yellow.svg)](http://amazon.fljsbook.com)

## Tabla de Contenidos

* [Prologo](prologo.md/#prologo)
* [Prefacio](prefacio.md/#prefacio)
* [Capítulo 1: ¿Porque Programacion Funcional?](ch1.md/#Capitulo-1-Porque-Programacion-Funcional)
    * [A un Vistazo](ch1.md/#a-un-vistazo)
    * [Confianza](ch1.md/#confianza)
    * [Comunicación](ch1.md/#comunicacion)
    * [Legibilidad](ch1.md/#legibilidad)
    * [Perspectiva](ch1.md/#perspectiva)
    * [Cómo Encontrar el Equilibrio](ch1.md/#como-encontrar-el-equilibrio)
    * [Recursos](ch1.md/#recursos)
* [Capítulo 2: La Naturaleza De Las Funciones](ch2.md/#chapter-2-the-nature-of-functions)
    * [¿Qué Es Una Función?](ch2.md/#what-is-a-function)
    * [Entrada De Funciones](ch2.md/#function-input)
    * [Argumentos Nombrados](ch2.md/#named-arguments)
    * [Salida de Funciones](ch2.md/#function-output)
    * [Funciones De Funciones](ch2.md/#functions-of-functions)
    * [Sintaxis](ch2.md/#syntax)
    * [¿Qué Es Esto (this)?](ch2.md/#whats-this)
* [Capítulo 3: Gestionando Entradas de Funciones](ch3.md/#chapter-3-managing-function-inputs)
    * [Todos Para Uno](ch3.md/#all-for-one)
    * [Adaptando Argumentos a Parámetros](ch3.md/#adapting-arguments-to-parameters)
    * [Algunos Ahora, Algunos Después](ch3.md/#some-now-some-later)
    * [Uno A La Vez](ch3.md/#one-at-a-time)
    * [El Orden Importa](ch3.md/#order-matters)
    * [Sin Puntos](ch3.md/#no-points)
* [Capítulo 4: Componiendo Funciones](ch4.md/#chapter-4-composing-functions)
    * [Salida a Entrada](ch4.md/#output-to-input)
    * [Composición General](ch4.md/#general-composition)
    * [Composición Reordenada](ch4.md/#reordered-composition)
    * [Abstracción](ch4.md/#abstraction)
    * [Revisitando Puntos](ch4.md/#revisiting-points)
* [Capítulo 5: Reduciendo Efectos Secundarios](ch5.md/#chapter-5-reducing-side-effects)
    * [Los Efectos A Un Lado, Por Favor](ch5.md/#effects-on-the-side-please)
    * [Una Vez Es Suficiente, Gracias](ch5.md/#once-is-enough-thanks)
    * [Pura Felicidad](ch5.md/#pure-bliss)
    * [Alli O No](ch5.md/#there-or-not)
    * [Purificando](ch5.md/#purifying)
* [Capítulo 6: Inmutabilidad de Valores](ch6.md/#chapter-6-value-immutability)
    * [Inmutabilidad Primitiva](ch6.md/#primitive-immutability)
    * [Valor A Valor](ch6.md/#value-to-value)
    * [Reasignación](ch6.md/#reassignment)
    * [Rendimiento](ch6.md/#performance)
    * [Tratamiento](ch6.md/#treatment)
* [Capítulo 7: Cierre vs Objeto](ch7.md/#chapter-7-closure-vs-object)
    * [La Misma Página](ch7.md/#the-same-page)
    * [Parecidos](ch7.md/#look-alike)
    * [Dos Caminos Divergen En Un Bosque...](ch7.md/#two-roads-diverged-in-a-wood)
* [Capítulo 8: Recursión](ch8.md/#chapter-8-recursion)
    * [Definición](ch8.md/#definition)
    * [Recursión Declarativa](ch8.md/#declarative-recursion)
    * [Pila](ch8.md/#stack)
    * [Reordenando La Recursión](ch8.md/#rearranging-recursion)
* [Capítulo 9: Operaciones de Lista](ch9.md/#chapter-9-list-operations)
    * [Procesamiento De Listas No-PF](ch9.md/#non-fp-list-processing)
    * [Map](ch9.md/#map)
    * [Filter](ch9.md/#filter)
    * [Reduce](ch9.md/#reduce)
    * [Operaciones De Lista Avanzadas](ch9.md/#advanced-list-operations)
    * [Método vs. Independiente](ch9.md/#method-vs-standalone)
    * [Buscando Por Listas](ch9.md/#looking-for-lists)
    * [Fusión](ch9.md/#fusion)
    * [Más Allá De Las Listas](ch9.md/#beyond-lists)
* [Capítulo 10: Asincronía Funcional](ch10.md/#chapter-10-functional-async)
    * [Tiempo Como Estado](ch10.md/#time-as-state)
    * [Ansioso vs Perezoso](ch10.md/#eager-vs-lazy)
    * [PF Reactiva](ch10.md/#reactive-fp)
* [Chapter 11: Poniendolo Todo Junto](ch11.md/#chapter-11-putting-it-all-together)
    * [Configuración](ch11.md/#setup)
    * [Eventos De Cotización](ch11.md/#stock-events)
    * [UI Cotizador Bursatil](ch11.md/#stock-ticker-ui)
* [Appendix A: Transducing](apA.md/#appendix-a-transducing)
    * [Why, First](apA.md/#why-first)
    * [How, Next](apA.md/#how-next)
    * [What, Finally](apA.md/#what-finally)
* [Appendix B: The Humble Monad](apB.md/#appendix-b-the-humble-monad)
    * [Type](apB.md/#type)
    * [Loose Interface](apB.md/#loose-interface)
    * [Just a Monad](apB.md/#just-a-monad)
    * [Maybe](apB.md/#maybe)
    * [Humble](apB.md/#humble)
* [Appendix C: FP Libraries](apC.md/#appendix-c-fp-libraries)
    * [Stuff to Investigate](apC.md/#stuff-to-investigate)
    * [Ramda](apC.md/#ramda-0230)
    * [Lodash/fp](apC.md/#lodashfp-4174)
    * [Mori](apC.md/#mori-032)
    * [Bonus: FPO](apC.md/#bonus-fpo)
    * [Bonus #2: fasy](apC.md/#bonus-2-fasy)