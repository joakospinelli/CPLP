# Sistemas de tipos

## 1. ¿Qué es un sistema de tipos y cuál es su función?

Un sistema de tipos es el conjunto de reglas que usa un lenguaje para clasificar los datos. A partir de un tipo de dato se pueda determinar cómo manipularlos, el conjunto de valores válido y qué operaciones son permitidas.

La función del sistema de tipos es garantizar la integridad de los programas, detectar errores y facilitar el entendimiento del código.

## 2. Definir y contrastar las definiciones de un sistema de tipos *fuerte* y *débil*. Ejemplificar con al menos 2 lenguajes para cada uno de ellos y justificar.

En un lenguaje fuerte o *fuertemente tipado*, las interacciones entre distintos tipos de datos son estrictas y no pueden realizarse automáticamente. Las operaciones y combinaciones de datos deben tener exactamente el tipo necesario, o de lo contrario darán un error. Estas verificaciones permiten reducir los errores en el programa debido a la incompatibilidad de tipos, aunque el programador debe conocer todas las restricciones posibles.

En un lenguaje *débilmente tipado*, los datos pueden cambiar de tipo automáticamente para poder interactuar con otros tipos de datos; esto permite que se puedan realizar operaciones entre tipos de datos que normalmente serían incompatibles, puesto que algunos de estos cambian implícitamente. Esto permite mayor flexibilidad al escribir el código, pero puede dar lugar a errores en los que la conversión automática no de los resultados deseados.

Ejemplos de lenguajes fuertes serían `Java` y `C`; los tipos de datos son verificados durante la compilación, por lo que darán error si se encuentran operaciones incompatibles. Las conversiones de tipos de datos debe realizarlas el programador explícitamente. Un ejemplo de esto sería la suma de un String con un número entero, que va a dar error salvo que se realice la conversión del número, por ejemplo con el método `toString()`.

Ejemplos de lenguajes débiles serían `JavaScript` y `PHP`; estos lenguajes no tienen restricciones para la interacción entre tipos, y realizan las conversiones implícitamente en caso de que sean necesarias. Un ejemplo de esto sería la suma entre un String y un número entero, que va a concatenar al entero al principio o al final de la cadena.

## 3. Además de la clasificación anterior, también es posible caracterizar el tipado como *estático* o *dinámico*. ¿Qué significa esto? Ejemplificar con al menos 2 lenguajes para cada uno de ellos y justificar.

En un tipado *estático*, el tipo de una variable se determina en la compilación y no puede cambiar durante la ejecución del programa. De esta manera, el compilador verifica la compatibilidad de una variable en las operaciones y asignaciones, para comprobar que no haya errores.

En el tipado *dinámico*, el tipo de una variable puede cambiar durante la ejecución del programa. Le brinda flexibilidad al lenguaje, puesto que la variable puede tomar valores de otros conjuntos de datos y realizar otras operaciones, pero puede dar lugar a errores si no se realizan las comprobaciones necesarias.

Ejemplos de lenguajes estáticos serían `Java` y `C`; en ambos lenguajes las variables se deben declarar con un identificador que represente a su tipo (como `int` o `double`), y este no puede cambiar en tiempo de ejecución. El compilador se encarga de comprobar las compatibilidades de tipos en las operaciones.

Ejemplos de lenguajes dinámicos serían `Python` y `JavaScript`; en estos lenguajes, las variables no deben declararse con un tipo explícito, y éste puede modificarse en tiempo de ejecución. Las comprobaciones de tipos para las operaciones se realizan en tiempo de ejecución.

# Tipos de datos

## 1. Dar una definición de tipo de dato.

Un tipo de dato es una clasificación definida en el sistema de tipos para representar a un conjunto de valores y operaciones que pueden realizarse con un dato concreto.

## 2. ¿Qué es un tipo predefinido elemental? Dar ejemplos.

Los tipos elementales son aquellos que están incorporados por el lenguaje de programación. Representan a los valores más básicos con los que se puede trabajar en el lenguaje.

Los tipos elementales más comunes son:
* Números enteros.
* Números reales.
* Caracteres.
* Booleanos.

## 3. ¿Qué es un tipo definido por el usuario? Dar ejemplos.

Los tipos definidos por el usuario son aquellos que el programador define a partir de un conjunto de datos elementales. Sirven para resolver problemas más concretos en un programa, por lo que su complejidad es mayor que la de los tipos elementales; además, sus compatibilidades y valores permitidos dependen totalmente de la implentación del programador.

Algunos ejemplos de tipos definidos por el usuario son:
* **Registros**: estructuras de datos agrupadas en una misma entidad.
* **Objetos**: poseen un estado y comportamiento definidos por el programador, instanciados a partir de una clase.
* **Enumeraciones:** conjunto de valores constantes.

# Tipos compuestos
## 1. Dar una breve definición de producto cartesiano *(en la bibliografía puede aparecer también como product type)*, correspondencia finita, uniones *(en la bibliografía puede aparecer también como sum type)* y tipos recursivos.

| Tipo compuesto | Descripción | Ejemplo |
| -------------- | ----------- | ------- |
| Producto cartesiano | Construcción que a partir de N conjuntos (que pueden ser datos u otros conjuntos) forma un nuevo conjunto compuesto por tuplas de N elementos, en la que cada elemento contiene combinación con los elementos de los conjuntos | Estructuras o registros: cada estructura está formada por 1..N elementos que pueden ser de diferentes tipos. |
| Correspondencia finita | Relación uno a uno entre dos conjuntos de datos. Esto implica que a cada elemento del conjunto A le corresponde exactamente un elemento del conjunto B y viceversa; los elementos no se pueden repetir ni omitir. | Arreglos: a cada elemento del arreglo le corresponde exactamente un índice numérico y viceversa (el índice siempre debe ser menor al tamaño del arreglo). |
| Unión | Construcción que combina varios tipos de datos en uno solo; representa a un tipo de datos en el que el valor puede ser de varios tipos distintos. | Tipos alternativos u opcionales. |
| Tipos recursivos | Tipos de datos que se definen a partir de sí mismos; tienen una referencia a sí mismos dentro de su definición. | Listas enlazadas; cada elemento contiene una referencia hacia el siguiente en la lista, que es del mismo tipo. |

## 2. Identificar a qué clase de tipo de datos pertenecen los siguientes extractos de código. En algunos casos puede corresponder más de una

<img src="./img/Practica 7/ej3.2.png">

# Mutabilidad e inmutabilidad

## 1. Definir mutabilidad e inmutabilidad respecto a un dato. Dar ejemplos en al menos 2 lenguajes.

La mutabilidad de un dato es la capacidad de modificar un dato después de que haya sido creado. Un dato es mutable si se puede modificar directamente su contenido después de crearlo, sin tener que crear un dato nuevo.

Un ejemplo de mutabilidad son las listas en Python:
```python
lista = [ 1, 2, 3 ]
lista[0] = 4

print(lista) # Salida: [ 4, 2, 3 ]
```
Una vez creada la lista, se puede acceder directamente a un elemento y modificarlo; todas las referencias a la lista van a percibir este cambio. Python ofrece tipos de datos mutables (listas, diccionarios, sets) e inmutables (números, Strings, tuplas).

Por otro lado, la inmutabilidad implica que un dato no puede modificarse luego de su creación. Todas los cambios que se le realicen sobre la variable requieren que se cree un dato nuevo y se asigne nuevamente.

Un ejemplo de imutabilidad son los Strings en Java:
```java
String a = "Hello";
a = a + " world";
System.out.println(a); // imprime "Hello world"
```
Si bien el String `a` se pudo modificar, internamente lo que se está haciendo es crear un nuevo objeto `String` con el valor de la concatenación, y luego se cambia la refencia de `a` hacia el nuevo objeto.

Otro ejemplo sobre la inmutabilidad es el método `freeze` en Ruby; por defecto, algunos objetos de Ruby son mutables (como los arrays), pero puede usarse el método `freeze` para volverlos inmutables:
```ruby
array = []
array.push(1, 2, 3)

array.each do |elem|
    puts elem # imprime [ 1, 2, 3 ]
end

array.freeze

array.push(4) # Error: can't modify frozen Array
```

## 2. Dado el siguiente código ¿Se puede afirmar entonces que el objeto “Dato.new(1)” es mutable? Justificar la respuesta sea por afirmativa o por la negativa.

```python
a = Dato.new(1)
a = Dato.new(2)
```
No se puede afirmar, porque al estar trabajando con objetos lo que se está haciendo es cambiar la referencia de `a` hacia un nuevo objeto de tipo `Dato`, pero no se está mutando al objeto original.

# Manejo de punteros

## 1. ¿Permite C tomar el l-valor de las variables? Ejemplificar.

Un puntero en C puede tomar el L-Valor de una variable usando el operador `&<nombre_variable>`. Esto permite tener un puntero con una referencia hacia una variable en específico, por lo que puede modificarse su valor sin accederla directamente.

```c
int main()
{
    int num = 5;
    int *puntero = &num; // toma el L-Valor de "num"
    
    *puntero = 10; // modifica el R-Valor en la dirección de &num
    
    printf("%d", num); // imprime 10
}
```

## 2. ¿Qué problemas existen en el manejo de punteros? Ejemplificar.

Algunos problemas que se podría tener con el manejo de punteros son:
* Por defecto los punteros se inicializan en `null`, implicando que no se les asignó una dirección una dirección de memoria; si se intenta acceder al valor al que apunta mientras está en `null` podría tener comportamientos no deseados.
```c
int main()
{
    int num = 5;
    int *puntero;
    
    printf("%d", *puntero);
}
```
* Podría tener un puntero de un tipo concreto trabajando sobre la dirección de una variable que es de otro tipo. Si no se realizan las comprobaciones necesarias, podría haber un error al intentar usar el puntero.
```c
int main()
{
    int num = 5;
    char *puntero = &num;
    
    printf("%d", *puntero);
}
```
* Se pueden realizar operaciones matemáticas sobre la dirección que tiene el puntero, por lo que se podría cambiar la referencia y terminar accediendo a una dirección de memoria no deseada.
```c
int main()
{
    int num = 5;
    int *puntero = &num;

    puntero = puntero + 10;
    
    printf("%p", puntero);
}
```

# TAD
## 1. ¿Qué características debe cumplir una unidad para que sea un TAD?

Un TAD (Tipo Abstracto de Datos) es un conjunto de datos y operaciones que se pueden realizar sobre un tipo de dato específico, sin saber los detalles de su implementación. El objetivo del TAD es abstraer al programador de los detalles internos de las estructuras, y que simplemente haga uso de estas a partir de interfaces definidas.

Un TAD está compuesto por dos partes:
* **Especificación:** describe los tipos de datos que se proporcionan y las operacioens que se pueden realizar sobre ellos. Se define cómo el programador puede acceder a las estructuras, sin dar detalles de su implementación.
* **Implementación:** define la manera en la que están compuestas internamente las estructuras y sus operaciones.

## 2. Dar algunos ejemplos de TAD en lenguajes tales como ADA, Java, Python, entre otros.

| Lenguaje | TAD | Explicación |
| -------- | --- | ----------- |
| Java | LinkedList | Lista enlazada. Cada elemento contiene un valor y una referencia hacia el siguiente en la lista. |
| Python | LifoQueue | Pila que almacena los datos en orden LIFO. |
| Ada | BinarySearchTree | Árbol binario de búsqueda. Cada elemento contiene un valor y referencias hacia su hijo izquierdo/derecho.