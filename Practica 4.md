# 1.
## a. Tome una de las variables de la línea 3 del siguiente código e indique y defina cuales son sus atributos:
```pascal
1. Procedure Practica4();
2. var
3.  a,i:integer
4.  p:puntero
5. Begin
6.  a:=0;
7.  new(p);
8.  p:= ^i
9.  for i:=1 to 9 do
10.     a:=a+i;
11. end;
12. ...
13. p:= ^a;
14. ...
15. dispose(p);
16. end;
```

| Nombre | Alcance | Tipo | R-Valor | L-Valor | TTL |
| ------ | ------- | ---- | ------- | ------- | --- |
| a | 3 - 16 | Integer | 0, 3, 6, 10, 15, 21, 28, 36, 45 | Automático | 1 - 16 |
| i | 3 - 16 | Integer | 1, 2, 3, 4, 5, 6, 7, 8, 9 | Automático | 1 - 16 |

## b. Compare los atributos de la variable del punto a) con los atributos de la variable de la línea 4. Que dato contiene esta variable?

La variable `p` es un puntero, por lo que su valor va a ser la dirección de memoria de otra variable. Su tiempo de vida también cambia, porque se usan las instrucciones `new` y `dispose` para crearlo y eliminarlo respectivamente.

| Nombre | Alcance | Tipo | R-Valor | L-Valor | TTL |
| p | 4 - 16 | Puntero | <dirección_i> <dirección_a> | Automático | 7 - 15 |

# 2.
## a. Indique cuales son las diferentes formas de inicializar una variable en el momento de la declaración de la misma.

Una variable puede inicializarse sin un valor asignado, o con un valor correspondiente al tipo de variable.

Si se inicializa sin valor, dependiendo el lenguaje se le puede asignar un valor predeterminado o asignarle el valor que quedó en el espacio de memoria que se le dio.

En algunos lenguajes, el valor inicial que se le da determina el tipo de la variable (por ejemplo, en JavaScript: `let x = 10` indica que 10 inicialmente va a ser `Number`, aunque pueda cambiar dinámicamente).

En los lenguajes orientados a objetos, los objetos se suelen iniciar con una palabra clave asociada al constructor de la clase a la que pertenecen, comunmente `new`.

## b. Analice en los lenguajes: Java, C, Python y Ruby las diferentes formas de inicialización de variables que poseen. Realice un cuadro comparativo de esta característica.

|   | Java | C | Python | Ruby |
| - | ---- | - | ------ | ---- |
| Con valor | int num = 0; | int num = 0; | num = 0 | num = 0 |
| Sin valor | int num; | int num; | **No se puede** (puede usarse `num = None`) | **No se puede** (puede usarse `num = nil`) |
| Objetos |  new Object(); | **No se puede** | Object() | Object.new() |

En los lenguajes fuertemente tipados (Java y C), vemos que incluso al asignarle un valor a la variable debemos declarar su tipo. Por otro lado, esta declaración permite que se puedan inicializar las variables sin un valor, cosa que en los debilmente tipados (Python y Ruby) no se puede, aunque se pueda asignar un valor nulo.

En los lenguajes orientados a objetos, la manera de inicializarlos es similar en todos: se usa el nombre de la clase y los paréntesis para enviarle los parámetros que estén definidos en el constructor.

# 3. Explique los siguientes conceptos asociados al atributo L-Valor de una:

* **Variable estática:** el L-Valor es fijo y se asigna en la compilación. Mantiene el mismo valor durante todo el programa.
* **Variable automática o semiestática:** la variable se genera dentro de una función y se destruye cuando termina. El L-Valor se asigna cuando comienza la función en tiempo de ejecución.
* **Variable dinámica:** el L-Valor se asigna y libera en tiempo de ejecución.
* **Variable semidinámica:** la variable se declara estáticamente, pero el L-Valor se asigna y libera en tiempo de ejecución.

## Investigue sobre que tipos de variables respecto de su L-Valor hay en los lenguajes C y Ada.

En ambos lenguajes, las variables pueden ser por valor o por referencia.
* Las variables por valor son aquellas que tienen su valor almacenado directamente en la dirección de memoria que tienen asignada.
* Las variables por referencia son aquellas que almacenan la dirección de memoria de otra variable; esto permite modificar la información de la otra variable usando un puntero.

# 4.
## a. ¿A qué se denomina variable local y a qué se denomina variable global?

Las variables locales son aquellas que su alcance está limitado a un bloque de código específico, por lo que sólo podrá ser usada dentro de ese contexto.

Las variables globales son las que tienen alcance en todo el programa.

## b. ¿Una variable local puede ser estática respecto de su L-Valor? En caso afirmativo dé un ejemplo

?

## c. Una variable global ¿siempre es estática? Justifique la respuesta.

No. Una variable estática es aquella que se crea una única vez en memoria y se mantiene igual durante toda la ejecución del programa; esto permite que cada vez que se utilice se esté haciendo referencia a la misma variable.

Lo que las diferencia de las variables globales es que las estáticas son declaradas dentro de un contexto, y sólo pueden ser accedidas dentro de éste. Por otro lado, las variables globales también pueden declararse como estáticas, y sólo van a poder ser modificadas dentro del programa principal en el que fueron declaradas.

## d. Indique qué diferencia hay entre una variable estática respecto de su L-Valor y una constante

Las variables con un L-Valor estático son aquellas que su dirección de memoria asignada va a ser la misma durante todo su tiempo de vida.

Las constantes son variables que su valor (R-Valor) es el mismo durante todo su tiempo de vida, pero esto es independiente de su ubicación de memoria.

# 5.
## a. En Ada hay dos tipos de constantes, las numéricas y las comunes. Indique a que se debe dicha clasificación.

Las constantes numéricas son aquellas que se usan para representar valor numéricos, ya sean números enteros o reales. Este tipo de constantes se almacenan directamente en la memoria del programa, por lo que ocupan espacio en el lenguaje compilado.

Las constantes comunes se usan para representar a todos los demás valores (booleanos, caracteres, strings, etc). Estas constantes también se resuelven en tiempo de compilación, pero se diferencian de las numéricas en que su valor se almacena en una tabla y se accede a ellas mediante referencias.

## b. En base a lo respondido en el punto a), determine el momento de ligadura de las constantes del siguiente código:
```ada
H: constant Float:= 3,5;
I: constant:= 2;
K: constant float:= H*I;
```

Todas las constantes son de tipo numérico, porque a pesar de que no se indique en todas se puede asumir por el tipo de dato asignado. Por lo t anto, la ligadura va a realizarse estáticamente durante la compilación.

# 6.  Sea el siguiente archivo con funciones de C:
```c
Archivo.c
{ 
    int x=1; (1)
    int func1();{
        int i;
        for (i:=0; i < 4; i++) x=x+1;
    }
    int func2();{
        int i, j;
        /*sentencias que contienen declaraciones y
        sentencias que no contienen declaraciones*/
        ......
        for (i:=0; i < 3; i++) j=func1 + 1;
    }
}
```
### Analice si llegaría a tener el mismo comportamiento en cuanto a alocación de memoria, sacar la declaración (1) y colocar dentro de func1() la declaración `static int x =1`.

Si se realiza ese cambio, la variable `x` va a pasar a ser estática para la función `func1()`; esto significa que va a almacenarse una única vez en memoria y siempre se va a usar la misma variable cada vez que se llame a la función.

Sin embargo, no cambiaría respecto a la alocación de memoria, puesto que las variables estáticas y globales tienen el mismo funcionamiento en cuanto a almacenamiento, a pesar de que el alcance de la variable sea distinto.

# 7. Sea el siguiente segmento de código escrito en Java, indique para los identificadores si son globales o locales.

```java
Clase Persona {
    public long id // global
    public string nombreApellido // global
    public Domicilio domicilio // global
    private string dni; // local
    public string fechaNac; // global
    public static int cantTotalPersonas; // global
    //Se tienen los getter y setter de cada una de las variables
    //Este método calcula la edad de la persona a partir de la fecha de nacimiento
    public int getEdad(){
        public int edad=0; // local
        public string fN = this.getFechaNac(); // local
        // ...
        return edad;
    }
}

Clase Domicilio {
    public long id; // global
    public static int nro // global
    public string calle // global
    public Localidad loc; // global
    //Se tienen los getter y setter de cada una de las variables
}
```
En Java, los identificadores de una clase son globales o locales dependiendo del encapsulamiento que se les dé (si son `public` son globales; si son `private` son locales). Los identificadores dentro de un método o estructuras de control son siempre locales.

Las variables estáticas son siempre globales porque están asociadas a la clase en sí, y no a una instancia particular.

*(el tipo de cada identificador está comentado en el código)*

# 8. Sea el siguiente ejercicio escrito en Pascal
```pascal
1-  Program Uno;
2-  type tpuntero= ^integer;
3-  var mipuntero: tpuntero;
4-  var i:integer;
5-  var h:integer;
6-  Begin
7-  i:=3;
8-      mipuntero:=nil;
9-      new(mipuntero);
10-     mipunterno^:=i;
11-     h:= mipuntero^+i;
12-     dispose(mipuntero);
13-     write(h);
14-     i:= h- mipuntero;
15- End.
```
## a. Indique el rango de instrucciones que representa el tiempo de vida de las variables i, h y mipuntero.

| Variable | TTL |
| -------- | --- |
| i | 1-15 |
| h | 1-15 |
| mipuntero | 9-12 |

## b. Indique el rango de instrucciones que representa el alcance de las variables i, h y mipuntero.

| Variable | Alcance |
| -------- | ------- |
| i | 4-15 |
| h | 5-15 |
| mipuntero | 3-15 |

## c. Indique si el programa anterior presenta un error al intentar escribir el valor de h. Justifique

No, porque el símbolo ^ de `mipuntero^` indica que se está usando el valor que se encuentra en la dirección almacenada en el puntero, y no la dirección en sí. Por lo tanto, al almacenar ese valor en `h` se está guardando dicho valor.

## d. Indique si el programa anterior presenta un error al intentar asignar a i la resta de h con mipuntero. Justifique

Esto sí va a tirar un error, porque el valor de `mipuntero` es una dirección de memoria, y por lo tanto no se puede restar con un entero.

## e. Determine si existe otra entidad que necesite ligar los atributos de alcance y tiempo de vida para justificar las respuestas anteriores. En ese caso indique cuál es la entidad y especifique su tiempo de vida y alcance.

La entidad restante sería la que identifica el tipo `tpuntero`, pero no sé cuál sería su TTL o su alcance.

## f. Especifique el tipo de variable de acuerdo a la ligadura con el L-Valor de las variables que encontró en el ejercicio.

| Variable | L-Valor |
| -------- | ------- |
| i | Automático |
| h | Automático |
| mipuntero | Automático |
| mipuntero^ | Dinámico |

**Aclaración:** para el puntero se declara tanto `mipuntero` como `mipuntero^` porque la asignación de memoria del puntero se realiza automáticamente, pero la dirección a la que apunta se puede cambiar dinámicamente, por eso hay que marcar la diferencia.

# 9. Elija un lenguaje y escriba un ejemplo:
* **a.** En el cual el tiempo de vida de un identificador sea mayor que su alcance
* **b.** En el cual el tiempo de vida de un identificador sea menor que su alcance
* **c.** En el cual el tiempo de vida de un identificador sea igual que su alcance

Está todo en la explicación práctica así que no lo hago 😴

# 10. Si tengo la siguiente declaración al comienzo de un procedimiento y ese procedimiento NO contiene definiciones de procedimientos internos. ¿Puedo asegurar que el alcance y el tiempo de vida de la variable “c” es siempre todo el procedimiento en donde se encuentra definida?. Analícelo y justifique la respuesta, para todos los casos.
```java
int c; // en C
var c: integer; // en Pascal
c: integer; // en ADA
```
El alcance y tiempo de vida de `c` van a ser de todo el procedimiento en el que la variable haya sido declarada.

Podría darse el caso en el que un procedimiento interno también declare una variable que se llame `c`, por lo que todas las referencias a ese identificador van a realizarse a la variable del procedimiento enterno; esto haría que el alcance de `c` global se reduzca. Sin embargo, en el enunciado se especifica que esto no pasa.

# 11.
## a. Responda Verdadero o Falso para cada opción. El tipo de dato de una variable es?
1. **Un string de caracteres que se usa para referenciar a la variable y operaciones que se pueden realizar sobre ella:** Falso.
2. **Conjunto de valores que puede tomar y un rango de instrucciones en el que se conoce el nombre:** Falso.
3. **Conjunto de valores que puede tomar y lugar de memoria asociado con la variable:** Verdadero; el lugar en memoria y cómo se realiza la asignación (estática, automática o dinámica) dependen del tipo de variable.
4. **Conjunto de valores que puede tomar y conjunto de operaciones que se pueden realizar sobre esos valores:** Verdadero.

## b. Escriba la definición correcta de tipo de dato de una variable.

El tipo de dato de una variable define el conjunto de valores válidos que puede contener y qué operaciones se pueden realizar con ella.

# 12. Sea el siguiente programa en ADA, completar el cuadro siguiente indicando para cada variable de que tipo es en cuanto al momento de ligadura de su L-Valor, su R-Valor al momento de alocación en memoria y para todos los identificadores cuál es su alcance y cual es su el tiempo de vida. Indicar para cada variable su R-Valor al momento de alocación en memoria

<img src="./img/Practica 4/p4ej12.png">

| Identificador | Tipo | R-Valor | Alcance | TTL |
| ------------- | ---- | ------- | ------- | --- |
| a (línea 4) | Automática | Basura | 4-14 | 1-14 |
| n (línea 4) | Automática | Basura | 4-14 | 1-14 |
| p (línea 4) | Automática | Basura | 4-14 | 1-14 |
| v1 (línea 5) | Dinámica | 0 | 5-14 |  1-14 |
| c1 (línea 6) | Estática | 10 | 6-14 | 1-14 |
| v2 (línea 7.2) | Dinámica | 0 | 7.2-7.6 | 7-7.6 |
| c1 (línea 7.3) | Automática | Basura | 7.3-7.6 | 7-7.6 |
| c2 (línea 7.3) | Automática | Basura | 7.3-7.6 | 7-7.6 |
| p (línea 4) | Dinámica | Basura | 7.4-7.6 | 7.5.3-7.5.6 |
| q (línea 4) | Dinámica | Basura | 7.4-7.6 | 7.5.3-7.5.8 |

# 13. El nombre de una variable puede condicionar:
* **Su tiempo de vida:** puede condicionarlo si al declarar la variable se agrega alguna palabra del lenguaje que incremente su tiempo de vida; por ejemplo, `static int edad`.
* **Su alcance:** no depende del nombre de la variable, pero sí de dónde esté declarada.
* **Su R-Valor:** su valor no depende del nombre de la variable.
* **Su tipo:** en lenguajes fuertemente tipados, el tipo de la variable se define al nombrarla junto con el tipo; por ejemplo, `String nombre`.
