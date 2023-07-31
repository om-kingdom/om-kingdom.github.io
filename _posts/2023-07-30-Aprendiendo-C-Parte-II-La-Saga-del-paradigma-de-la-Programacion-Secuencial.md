--- 
layout: post
title: "Aprendiendo C Parte II: La $aga del Paradigma de la Programacion Secuencial"
date: 2023-07-30 20:34:42 +0100
categories: "C"
---


# Aprendiendo C Parte II: La $aga del Paradigma de la Programación Secuencial
#C #ProgramacionSecuencial

# El paradigma de la programación Secuencial
Comencemos definiendo qué es la programación secuencial:
La programación secuencial es el paradigma de programación más básico y común en la programación, y al hablar de una estructura secuencial nos estamos refiriendo simplemente a un bloque de código que sigue una secuencia lineal y ordenada de instrucciones que se ejecutan una tras otra.

En un programa escrito en paradigma de programación secuencial, las instrucciones se ejecutan secuencialmente en el orden en el que aparecen en elcódigo fuente, sin bifurcaciónes ni repeticiones. Cada instrucción se ejecuta solo después de que la anterior se haya completado.

La estructura secuencial es la base sobre la cuál se construyen estructuras de control más complejas como las estructuras de selección (if, else) y las estructuras de control de repetición (for, while). Estas estructuras permiten al programador tomar decisiones y repetir acciones según ciertas condiciones, lo que agrega flexibilidad y complejidad al flujo de ejecución del programa. Sin embargo, la programación secuencial sigue siendo una parte fundamental en la mayoría de los programas, ya que muchos algoritmos y tareas se pueden resolver utilizando una secuencia lineal y ordenada de datos.

# Ejemplo

Con el fin de ejemplificar mejor lo anterior mencionado, se realizará un código en base a un problema sencillo, por supuesto escrito en lenguaje C.

## Problema 
Realizar la carga de dos números decimales por teclado e imprimir su suma y producto.

## Análisis del problema
Nos encontramos con un problema relativamente sencillo de analizar, pues solo se necesitan dos variables numéricas para realizar las operaciones de suma y producto. Los valores de las dos variables numéricas deberán ser recibidas por teclado, es decir, el usuario le otorga los valores al programa. Los dos resultados (suma y producto) deben ser almacenados en una variable para cada uno, posterior a su calculo, los resultados deberán mostrarse en pantalla. 
Observamos que no hay estructuras condicionales ni repetitivas, por lo cual este sencillo ejemplo entra dentro de la categoria de programación secuencial.

## Diseño de la solución
#stdio
Para dar solución al problema planteado, haremos uso de la biblioteca _stdio_ del lenguaje C. A continuación una breve explicación de esta bibilioteca:
La biblioteca _stdio_ (standard input/output) es una de las bibliotecas estándar más importantes en el lenguaje de programación C.
Proporciona una amplia gama de funciones para realizar operaciones de entrada y salida de datos. La biblioteca stdio permite a los programadores interactuar con el sistema de archivos, la entrada y salida estándar y realizar operaciones de lectura y escritura de datos.
Las funciones de la biblioteca _stdio_ que utilizaremos en esta ocasión serán las siguientes:

1. _printf()_: Esta función se utiliza para imprimir texto y datos formateados en la salida estándar (generalmente, la pantalla). Permite mostrar mensajes, variables, y otros datos en diferentes formatos mediante _especificadores de formato_.
2. _scanf()_: Es utilizada para leer datos formateados de la entrada estándar (genrealmente, el teclado). Con _scanf()_, los programadores pueden capturar y almacenar datos ingresados por el usuario en variables.

La librería _stdio_ está incluida en el archivo de encabezado <stdio.h>, por lo que es necesario incluir este encabezado en el código fuente para utilizar sus funciones.
Ademas de eso requerimos de 4 variables de tipo _float_. En C, el tipo de datos _float_ se utiliza para representar números en coma flotante con punto decimal. Es decir, números que tienen una parte fraccional, lo que significa que pueden tener decimales. Estos números se representan utilizando el estándar IEEE 754 en la mayoría de implementaciones de C. Para mayor información  respecto al estándar IEEE 754 revisa la sección de  _Notas adicionales_ de ste post.

El tipo __float__ en C tiene una precisión limitada en comparación con otros tipos de datos como __double__. Un número __float__ ocupa típicamente 4 bytes de memoria y puede representar valores con aproximadamente 7 dígitos. Bastante útil para el problema planteado en esta ocasión.

Continuando con las variables; las 4 variables de tipo float que utilizaremos en esta ocasión serán las siguientes:

- flaot numero1: Para almacenar el primer número introducido por el usuario.
- float numero2: Para almacenar el segundo número introducido por el usuario.
- float resultadoSuma: Para almacenar el resultado de las uma de los dos números.
- float resultadoProducto: paa almacenar el resultado de la operación producto de los dos números.

__Para nombrar variables se recomienda utilizar nombres descriptivos y evitar abreviaturas confusas.__


Antes de continuar es importante mencionar los especificadores de formato en C.

# Especificadores de formato en C
#especificadoresDeFormato

Un especificador de formato en C es un código especial utilizado para controlar el formato de entrada y salida de datos al utilizar funciones como `printf()` y `scanf()`. Estos códios especiales comienzan con el símbolo de porcentaje (`%`) y están seguidos de un carácter que representa el tipo de dato que se formateará.
Es importante utilizar los especificadores de formato adecuados según el tipo de dato que se está manipulando para evitar errores de interpretación o comportamientos inesperados en el programa. también es posible utilizar modificadores de longituf y precisión junto con los especificadores de formato para ajustar aún más el formato de los datos de acuerdo con las necesidades especificas.

Especificadores de formato para `printf()` (salida de datos):
- `%d`: Entero con signo (int).
- `%u`: Entero sin signo (unsigned int).
- `%f`: Número de punto flotante (float).
- `%lf`: Número de punto flotante de doble precisión (double).
- `%c`: Carácter (char).
- `%s`: Cadena de caracteres (string).
- `%x`, `%X`: Entero hexadecimal en minúscilas o mayúsculas.
- `%o`: Entero en octal.
- `%p`: Puntero (dirección de memoria).
- `%%`: Para imprimir el símbolo de porcentaje literal (%).

Especificadores de formato para `scanf()` (entrada de datos):
- `%d`: Entero con signo (int).
- `%u`: Entero sin signo (unsigned int).
- `%f`: Número de punto flotante (float).
- `%lf`: Número de punto flotante de doble precisión (double).
- `%c`: Carácter (char).
- `%s`: Cadena de caracteres (string).
- `%x`, `%X`: Entero hexadecimal en minúscilas o mayúsculas.
- `%o`: Entero en octal.
- `%p`: Puntero (dirección de memoria).

# Implementación de la solución

Con un anpalisis y diseño adecuado podemos proceder a la implementación de la solución, es decir, escribir código.

```c
//libreria standard input/output
#include <stdio.h>


int main(){
    //declaracion de las variables a utilizar
    float numero1, numero2, resultadoSuma, resultadoProducto;

    //se inicializan los valores de los numeros con valores dados por el usuario
    printf("\nIntroduce el primer número: ");
    scanf("%f", &numero1);
    printf("\nIntroduce el segundo número: ");
    scanf("%f", &numero2);

    /*
    * En las sentencias scanf() se agrega el operador de direcección & para almacenar el valor leido en una variable.
    *El operador de dirección se utiliza para obtener la dirección de memoria de una variable.
    */ 
    
    //Se realizan las operaciones de suma y producto
    
    resultadoSuma = numero1 + numero2;
    resultadoProducto = numero1 * numero2;

    //Se muestran los resultados en pantalla 
    printf("\nEl resultado de ña suma es: %f", resultadoSuma);
    printf("\nEl producto es: %f", resultadoProducto);
    return 0;
}
```
Teniendo como ejecución la siguiente:

```
Introduce el primer número: 5.2

Introduce el segundo número: 2

El resultado de la suma es: 7.200000
El producto es: 10.400000
Process finished with exit code 0
```

# Notas adicionales
## Estándar IEEE 754

El estándar IEEE 754 es un conjunto de especificaciones desarrolladas por el Instituto de Ingenieros Eléctricos y Electrónicos (Institute of Electrical and Electronics Engineers, IEEE) que define el formato de representación y las operaciones aritméticas para números en coma flotante. Fue publicado por primera vez en 1985 y se ha convertido en el estándar ampliamente aceptado para la representación de números de punto flotante en computadoras y sistemas electrónicos.

El estándar IEEE 754 define dos formatos principales de representación de números en coma flotante: precisión simple (single precision) y precisión doble (double precision). Estos formatos se utilizan para representar números de punto flotante en sistemas de hardware y software.

En el formato de precisión simple (single precision), un número en coma flotante ocupa 32 bits y se divide en tres componentes:

- Signo: Un solo bit que indica si el número es positivo o negativo. 0 representa un número positivo y 1 representa un número negativo.

- Exponente: Un grupo de 8 bits que representa el exponente del número en base 2. Permite que el número sea escalado y ajustado en el rango requerido.

- Mantisa: Un grupo de 23 bits que representa la parte fraccional (mantisa) del número. También se conoce como la fracción o la parte significativa.

El formato de precisión doble (double precision) ocupa 64 bits y es similar al formato de precisión simple, pero con una mayor precisión y rango, ya que utiliza 11 bits para el exponente y 52 bits para la mantisa.

El estándar IEEE 754 también define las operaciones aritméticas básicas (suma, resta, multiplicación y división) para números en coma flotante y proporciona reglas para el redondeo y manejo de casos especiales, como el desbordamiento y el resultado de operaciones indefinidas.

El uso del estándar IEEE 754 garantiza la portabilidad y consistencia en la representación de números de punto flotante entre diferentes sistemas y arquitecturas, lo que es esencial para el correcto funcionamiento de cálculos científicos y aplicaciones que requieren precisión en el manejo de números reales.

