---
layout: post 
title: "Aprendiendo C Parte III: La $aga de la Compilación y Ejecución"
date: 2023-09-08 15:53:58 +0100
categories: "C"
---
# Aprendieno C Parte III: La $aga de la Compilación y Ejecución
#C #Compilar #Ejecutar 

En el articulo de hoy hablaremos sobre la compilación y ejecución de programas escritos en lenguaje C.
Pero antes de comenzar, debemos agregar un nuevo paradigma a nuestro repertorio de habilidades como programadores: Programación imperativa.
# Programación imperativa
Partiendo del hecho de que ya estamos familiarizados con la programación secuencial, comprender la programación imperativa no debería ser complicado. La programación imperativa es un paradigma de programación que se centra en dar instrucciones detalladas al ordenador sobre como realizar una tarea.
A diferencia de la programación secuencial, que sigue un flujo lineal de ejecución de instrucciones, la programación imperativa permite un mayor control sobre el flujo de ejecución mediante el uso de estructuras de control y variables para manipular datos y tomar decisiones.
A continuación algunos conceptos clave de la programación imperativa:
1. Secuencialidad: Aunque la programación imperativa permite un mayor control sobre el flujo del programa, sigue siendo secuencial en su naturaleza. Las instrucciones se ejecutan en el orden en el que se escriben, a menos que se utilicen estructuras de control para cambiar ese orden.
2. Estructuras de Control: Las estructuras de control, como los bucles y las sentencias condicionales (if-else), son fundamentales en la programación imperativa. Estas estructuras permiten controlar el flujo del programa. Se puede usar, por ejemplo, un bucle para repetir una serie de instrucciones varias veces o utilizar una secuencia condicional para tomar decisiones basadas en ciertas condiciones.
Con esto claro, podemos afirmar que C es un lenguaje de programación imperativa.
Continuando con el recorrido de hoy, ejemplificaremos lo anterior con un código.

``` C
───────┬───────────────────────────────────────────────────────────────────────────────
       │ File: comenzando.c
───────┼───────────────────────────────────────────────────────────────────────────────
   1   │ #include <stdlib.h>
   2   │ #include <stdio.h>
   3   │ 
   4   │ // La cosa principal que este programa hace
   5   │ int main(void){
   6   │   // Declaraciones
   7   │   double A[5] = {
   8   │     [0] = 9.0,
   9   │     [1] = 2.9,
  10   │     [4] = 3.E+25, 
  11   │     [3] = .00007, 
  12   │   };
  13   │ 
  14   │   // Haciendo algo de trabajo
  15   │   for (size_t i = 0; i < 5; i++){
  16   │     printf("elemento %zu es %g \tsu cuadrado es %g\n", 
  17   │         i, 
  18   │         A[i], 
  19   │         A[i] * A[i]);
  20   │   }
  21   │   return EXIT_SUCCESS;
  22   │ }
───────┴───────────────────────────────────────────────────────────────────────────────

```

```bash
───────┬───────────────────────────────────────────────────────────────────────────────
       │ Terminal
───────┼───────────────────────────────────────────────────────────────────────────────
   0   │ ❯ ./comenzando
   1   │ elemento 0 es 9       su cuadrado es 81
   2   │ elemento 1 es 2.9       su cuadrado es 8.41
   3   │ elemento 2 es 0         su cuadrado es 0
   4   │ elemento 3 es 7e-05     su cuadrado es 4.9e-09
   5   │ elemento 4 es 3e+25     su cuadrado es 9e+50
───────┴───────────────────────────────────────────────────────────────────────────────

```

Fácilmente podemos identificar dentro de nuestro programa las parques que el texto en este programa muestra: la parte en la línea 16 que se encuentra entre comillas. La acción real ocurre entre esa línea y la linea 19. C llama a esto un _statement_. Otros lenguajes utilizan el termino _instrucción_ que describe mejor su propósito. Este _statement_ en particular es una _llamada_ a una _función_ llamada __printf__:

``` c
───────┬───────────────────────────────────────────────────────────────────────────────
       │ File: comenzando.c
───────┼───────────────────────────────────────────────────────────────────────────────
  16   │     printf("elemento %zu es %g \tsu cuadrado es %g\n", 
  17   │         i, 
  18   │         A[i], 
  19   │         A[i] * A[i]);
───────┴───────────────────────────────────────────────────────────────────────────────
```

La función __printf__ recibe cuatro _argumentos_, colocados dentro de un par de _párentesis_, ( . . . ):
- El texto entre las comillas es lo que se conoce como una _string literal_ que sirve como un _formato_ para la salida. Dentro del texto encontramos tres marcadores (_especificadores de formato_) que indican las posiciones en la salida donde deben colocarse los números. Esos marcadores comienzan con un carácter de porcentaje %. Este formato además contiene algunos _caracteres de escape_ que comienzan con la una diagonal invertida: __\t__ y __\n__.
- Después del carácter de coma en la linea 16 nos encontramos con la letra __i__. Este valor será impreso en el lugar del primer especificador de formato, %zu.
- Otra coma separa el siguiente argumento __A[i]__. Este valor será impreso en el lugar del segundo especificador de formato, el primer __%g__.
- Al final, una vez más separado por una coma, aparece __A[i] * A[i]__ que corresponde al último __%g__.
Al final de este articulo, en la sección de Notas adicionales hay información extra respecto a los especificadores de formato y la librería stdlib.

De momento solo destacaremos que el funcionamiento principal del programa es imprimir algunas lineas en la terminal, y eso lo "ordena" la función __printf__ que es utilizada para este fin. Lo demás son particularidades para especificar que numeros serán impresos y cuantos de ellos.

# Compilación y ejecución.
Como vimos en la sección anterior, el programa en texto le indica a la computadora lo que queremos hacer. Como tal es solo otra pieza de texto que hemos escrito y almacenado en algún lugar en nuestra unidad de almacenamiento, pero el programa en texto como tal no puede ser entendido por nuestra computadora. Hay un programa especial llamado _compilador_, que traduce el texto en C en algo que nuestra máquina puede comprender: el _código binario_ o _ejecutable_. La forma en la que se ve el programa traducido y como la traducción es realizada son bastante complicados para explicar en este breve articulo. Un libro entero dedicado a eso sería la forma adecuada de explicar estos conceptos. De cualquier manera, de momento, no necesitamos comprender más a profundidad, ya que tenemos la herramienta que hace todo el trabajo por nosotros.

Nota: _C es un lenguaje de programación compilado._

El nombre del compilador y sus argumentos dados en la línea de comandos depende mucho de la _plataforma_ en la que ejecutemos nuestro programa. La razón de esto es bastante sencilla: el código binario al que se espera llegar _depende de la plataforma_: esto es, su forma y detalles dependen de la computadora en la que se desea ejecutar. Una PC tiene distintas necesidades que un teléfono, por ejemplo. De hecho, esa es una de las razones por las que C existe: C provee un nivel de abstracción para todas los diferentes lenguajes específicos para cada maquina, habitualmente conocido como __ensamblador__.

Nota: _Un programa C correcto es portable entre distintas plataformas._

El trabajo del compilador es asegurarse de que nuestros programas de texto, una vez traducidos para la plataforma adecuada, se ejecutarán correctamente en tu PC, tu teléfono y tal vez en tu refrigerador.
Con eso dicho, si posees un sistema POSIX (tales como Linux o macOS), existe la posibilidad de que un programa llamado c99 se encuentre presente y eso es en realidad un compilador de C. Tratemos de compilar el programa de ejemplo usando el siguiente comando:

# Comenzando

```bash
───────┬───────────────────────────────────────────────────────────────────────────────
       │ Terminal
───────┼───────────────────────────────────────────────────────────────────────────────
   0   │❯ c99 -Wall -o comenzando comenzando.c -lm
───────┴───────────────────────────────────────────────────────────────────────────────
```

El compilador debería hacer su trabajo sin problemas y entregar un archivo ejecutable llamado _comenzando_ en el directorio actual. En la linea de ejemplo,
- _c99_ el programa compilador.
- _-Wall_ le dice al compilador que nos advierta si encuentra algo inusual.
- _-o comenznado_ le indica que debe almacenar la _salida del compilador_ en un archivo llamado _comenzando_.
- _comenzando.c_ nombre el _archivo fuente_ que contiene el código en C que hemos escrito. Es importante notar que la extensión .c al final del nombre del archivo se refiere al lenguaje de programación C.
- _-lm_ le dice al programa compilador que agrege algunas funciones matemáticas estándar en caso de ser necesario; las necesitaremos después.
Ahora podemos _ejecutar_ nuestro recién creado _ejecutable_. Escribamos

``` bash
───────┬───────────────────────────────────────────────────────────────────────────────
       │ Terminal
───────┼───────────────────────────────────────────────────────────────────────────────
   0   │❯ ./comenzando
───────┴───────────────────────────────────────────────────────────────────────────────
```

Y se mostrará exactamente la misma salida que mostramos anteriormente. Eso es lo que signfica _portable_: Donde sea que ejecutes ese programa, su _comportamiento_ debería ser el mismo.
En caso de que no hayas tenido suerte y el comando de compilación no funciona, tendrás que ver el nombre de tu _compilador_ que se encuentra en la documentación del sistema. Incluso quizás tengas que instalar un compilador si ninguno está disponible. Los nombre de los compiladores varían. Aquí hay algunas alternativas comunes que podrían ayudar:

``` bash
───────┬───────────────────────────────────────────────────────────────────────────────
       │ Terminal
───────┼───────────────────────────────────────────────────────────────────────────────
   0   │❯ clang -Wall -lm -o comenzando comenzando.c
   1   │❯ gcc -std=c99 -Wall -lm -o comenzando comenzando.c
   3   │❯ icc -std=c99 -Wall -lm -o comenzando comenzando.c
───────┴───────────────────────────────────────────────────────────────────────────────
```

Algunos de estos compiladores, incluso si están presentes en tu computadora, podrían no compilar el programa sin problemas. Con el programa presentado anteriormente mostramos un mundo ideal: un programa que funciona y produce los mismos resultados en todas las plataformas. Desafortunadamente, cuando programamos por nuestra cuenta, a menudo tendremos un programa que funciona solo parcialmente y que podría producir resultados incorrectos o poco confiables. Por lo tanto, veamos el siguiente ejemplo de un programa en texto que se ve similar al anterior.
Si ejecutamos el compilador con el siguiente programa, debería darnos alguna información de __diagnostico__.

``` c
───────┬───────────────────────────────────────────────────────────────────────────────────────
       │ File: programa_con_errores.c
───────┼───────────────────────────────────────────────────────────────────────────────────────
   1   │ // La cosa ṕrincipal que este programa hace
   2   │ void main(){
   3   │   //Declaraciones 
   4   │   int i;
   5   │   double A[5] = {
   6   │     9.0, 
   7   │     2.9, 
   8   │     3.E+25, 
   9   │     .00007, 
  10   │   };
  11   │ 
  12   │   // Haciendo algo de trabajo 
  13   │   for (i = 0; i < 5; i++){
  14   │     printf("Elemento %d es %g \tsu cuadrado es %g\n", 
  15   │         i, 
  16   │         A[i], 
  17   │         A[i] * A[i]);
  18   │   }
  19   │   return 0;
  20   │ }
───────┴─────────────────────────────────────────────────────────────────────────────────────────────

```

``` bash
───────┬───────────────────────────────────────────────────────────────────────────────
       │ Terminal
───────┴───────────────────────────────────────────────────────────────────────────────
❯ c99 -Wall -o programa_con_errores programa_con_errores.c
programa_con_errores.c:2:6: aviso: el tipo de devolución de ‘main’ no es ‘int’ [-Wmain]
    2 | void main(){
      |      ^~~~
programa_con_errores.c: En la función ‘main’:
programa_con_errores.c:14:5: aviso: declaración implícita de la función ‘printf’ [-Wimplicit-function-declaration]
   14 |     printf("Elemento %d es %g \tsu cuadrado es %g\n",
      |     ^~~~~~
programa_con_errores.c:1:1: nota: include ‘<stdio.h>’ or provide a declaration of ‘printf’
  +++ |+#include <stdio.h>
    1 | // La cosa ṕrincipal que este programa hace
programa_con_errores.c:14:5: aviso: declaración implícita incompatible de la función interna ‘printf’ [-Wbuiltin-declaration-mismatch]
   14 |     printf("Elemento %d es %g \tsu cuadrado es %g\n",
      |     ^~~~~~
programa_con_errores.c:14:5: nota: incluya ‘<stdio.h>’ o proporcione una declaración de ‘printf’
programa_con_errores.c:19:10: aviso: ‘return’ con valor, en una función que devuelve void [-Wreturn-type]
   19 |   return 0;
      |          ^
programa_con_errores.c:2:6: nota: se declara aquí
    2 | void main(){
      |      ^~~~
────────────────────────────────────────────────────────────────────────────────────────────
```

Tenemos muchas lineas de "advertencia" bastante extensas. Al final el compilador generó un ejecutable. Sin embargo, la salida cuando ejecutamos el programa es diferente. Esto es una señal de que debemos ser cuidadosos y poner atención a los detalles.
_clang_ es incluso más  quisquilloso y nos proporciona lineas de diagnostico más extensas:

```bash
───────┬───────────────────────────────────────────────────────────────────────────────
       │ Terminal
───────┴───────────────────────────────────────────────────────────────────────────────
❯ clang -Wall -o programa_con_errores programa_con_errores.c
programa_con_errores.c:2:1: warning: return type of 'main' is not 'int' [-Wmain-return-type]
void main(){
^
programa_con_errores.c:2:1: note: change return type to 'int'
void main(){
^~~~
int
programa_con_errores.c:14:5: error: call to undeclared library function 'printf' with type 'int (const char *, ...)'; ISO C99 and later do not support implicit function declarations [-Wimplicit-function-declaration]
    printf("Elemento %d es %g \tsu cuadrado es %g\n", 
    ^
programa_con_errores.c:14:5: note: include the header <stdio.h> or explicitly provide a declaration for 'printf'
programa_con_errores.c:19:3: error: void function 'main' should not return a value [-Wreturn-type]
  return 0;
  ^      ~
1 warning and 2 errors generated.
────────────────────────────────────────────────────────────────────────────────────────────
```

¡Esto es excelente! Es una _salida de diagnostico_ que es más informativa. En particular nos da dos pistas: esperaba un tipo de retorno distinto para __main__, y esperaba que nosotros tuviéramos una linea como lo es la línea 2 del primer programa en texto de ejemplo, para especificar de donde proviene la función __printf__. Observemos como _clang_, a diferencia de _cgg_ no produjo ningún ejecutable. El compilador considera fatal el problema en la línea 19.
Dependiendo de la plataforma, podemos forzar al compilador para rechazar programas que produzcan tales diagnosticos. Para _cgg_ tal opción en la linea de comandos sería __-Werror__.
Así que hemos visto dos de los puntos en los que `comenzando.c` y `programa_con_errores.c` son diferentes, y esas dos modificaciones volvieron un buen programa y portable conforme a los estándares en un mal programa.
Además vimos que el compilador está aquí para ayudarnos. Señala el problema en las líneas dentro del programa que causan los conflictos, y con un poco de experiencia podremos comprender lo que nos dice.

Nota: _Un programa en C debería compilar limpiamente y sin advertencias._

# Conclusiones
Finalmente podemos recalcar los siguientes puntos:
- C esta diseñado para darle ordenes a la computadora. Por lo tanto es un intermediario entre nosotros (los programadores) y las computadoras.
- C debe ser compilado para ejecutarse. El compilador provee la traducción entre el lenguaje que nosotros entendemos (C) y las necesidades especificas de cada plataforma en particular.
- C otorga un nivel de abstracción que proporciona portabilidad. Un programa en C puede ser utilizado en muchas y distintas arquitecturas de computadoras.
- El compilador de C está aquí para ayudarnos. Si te advierte acerca de algo en tu código, escuchalo.
# Notas adicionales
- En C, la biblioteca "_stdlib_" (que significa "standard library") es una parte esencial del lenguaje y proporciona un conjunto de funciones y macros que son fundamentales para muchas tareas comunes en programación. La librería "_stdlib_" incluye diversas funciones y constantes que se utilizan para manipular memoria, realizar conversiones de datos, generar números aleatorios y otras tareas esenciales.
- La elección de utilizar __'EXIT_SUCCESS'__ en lugar de simplemente __'return 0'__ es una cuestión de claridad y portabilidad de código. __'EXIT_SUCCESS'__ es una constante definida en la biblioteca estándar de C, específicamente en la "stdlib.h". __'EXIT_SUCCESS'__ hace que el código sea más legible y más portátil, ya que se adapta automáticamente al valor de éxito definido por la plataforma en la que se ejecuta el programa.
- __size_t__ es n tipo de datos que se utiliza comúnmente en el lenguaje de programacion C y C++. Es un tipo de datos sin signo, lo que significa que solo puede representar números enteros no negativos. Es útil para representar tamaños de objetos en memoria, ya que los tamaños de memoria nunca pueden ser negativos. El tamaño y el rango de __size_t__ dependen de la plataforma y del sistema en el que se esté utilizando el lenguaje C. En sistemas de 32 bits generalmente tiene un tamaño de 4 bytes (32 bits) y en sistemas de 64 bits suele tener un tamaño de 8 bytes (64 bits), por lo tanto puede representar tamaños de objetos en memoria que son apropiados para la arquitectura del sistema en el que se ejecuta el programa. La utilidad principal de __size_t__ es representar tamaños de objetos en memoria, como el tamaño de matrices, la longitud de cadenas de caracteres, el número de elementos en un arreglo, o la cantidad de bytes necesarios para almacenar una estructura de datos. Al utilizar __size_t__ se puede escribir código más portátil ya que se adapta automáticamente al tamaño de la plataforma en la que se compila.
- __%zu__ es un especificador de formato utilizado para imprimir valores de tipo _size_t_.
- __%g__ es un especificador de formato utilizado para imprimir valores en notación decimal o en notación exponencial.
