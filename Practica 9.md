# 1. Una sentencia puede ser simple o compuesta, ¿Cuál es la diferencia?

Las sentencias simples son aquellas que están formadas por una única instrucción.

Por el contrario, las sentencias compuestas están formadas por dos o más instrucciones unidas en un único bloque de código, agrupadas usando algún delimitador definido por el lenguaje (generalmente `{ }` o `begin...end`).

# 2. Analice como C implementa la asignación.

La asignación en C se realiza con la instrucción `a = b`, en la que a la variable `a` se le asigna el valor de `b`, que puede ser un valor, otra variable, una expresión o el llamado a una función.

```c
int a = 1; // asignación con valor primitivo

int b;
b = a + 1; // asignación con expresión. b = 1
```

# 3. ¿Una expresión de asignación puede producir efectos laterales que afecten al resultado final, dependiendo de cómo se evalúe? De ejemplos.

El resultado final se puede ver alterado dependiendo de cómo se evalúan las expresiones al momento de la asignación.

Un buen ejemplo de un efecto colateral es el operador `++` en C. Si se usa después del nombre de la variable (`a++`), va a retornar el valor de la variable y luego la va a incrementar; si se usa antes del nombre (`++a`), primero la va a incrementar y luego va a retornar el valor.

```c
int main()
{
    int a = 0;
    int b = a++; // asigna 0 e incrementa 'a'
    
    printf("%d\n", b); // imprime 0
    printf("%d\n", a); // imprime 1
    
    a = 0;
    int c = ++a; // incrementa 'a' y asigna 1
    
    printf("%d\n", c); // imprime 1
    printf("%d\n", a); // imprime 1
}
```

Otra condición que podría dar resultados no deseados es el orden de evaluación de las expresiones; si se evalúan de izquierda a derecha podrían dar un resultado distinto que si lo hacen al revés:
```c
int main()
{
    int a = 0;
    int b = 1;
    int c = 2;
    
    a = b = c;
    
    printf("%d - %d - %d", a, b, c); // imprime '2 - 2 - 2'
}
```
En el caso de C, las asignaciones se realizan de derecha a izquierda; esto quiere decir que primero va a obtener el valor de `c` y asignarlo a `b`, luego va a obtener el valor de `b` (que ahora es el mismo que `c`) y asignarlo a `a`. Si se realizaran en el orden inverso, el resultado sería `0 - 0 - 0`.

# 4. Qué significa que un lenguaje utilice circuito corto o circuito largo para la evaluación de una expresión. De un ejemplo en el cual por un circuito de error y por el otro no.

*Circuito corto* o *circuito largo* son conceptos que indican la manera en la que un lenguaje evalúa las condiciones booleanas.

Un lenguaje es de circuito corto si puede terminar su ejecución sólo con leer la primer expresión de una condición booleana compuesta, teniendo en cuenta el operador lógico. Esto se basa en los siguientes casos:
* Si la primer expresión de una operación lógica `AND` es falsa, el resultado siempre va a ser falso; entonces devuelve falso sin revisar el resto.
* Si la primer expresión de una operación lógica `OR` es verdadera, el resultado siempre va a ser verdadero; entonces devuelve verdadero sin revisar el resto.

Un lenguaje es de circuito largo si, independientemente del resultado de la primer expresión, revisa toda una condición booleana antes de retornar el resultado.

El ejemplo lo podemos demostrar en Java, puesto que permite usar los dos tipos de circuito usando `&&` para el circuito corto y `&` para el circuito largo:
```java
    public static void main(String[] args) {
        int a = 10;
        int b = 0;

        if (b != 0 && a / b > 5) {
            System.out.println("Circuito corto");
        }

        if (b != 0 & a / b > 5) {
            System.out.println("Circuito largo");
        }
    }
```
En este ejemplo, el circuito corto va a terminar de evaluar la condición al ver que la expresión `b != 0` es falsa.

Por otro lado, el circuito largo va a evaluar toda la expresión booleana y va a realizar la división `a / b` para evaluar el segundo término; como `b` es 0, va a producirse un error de división por 0.

# 5. ¿Qué regla define Delphi, Ada y C para la asociación del `else` con el `if` correspondiente? ¿Cómo lo maneja Python?

En Delphi, Ada y C, el `else` se corresponde con el `if` más cercano que todavía no tenga un `else` ya correspondido.

Python, a diferencia de los anteriores, se basa en el indentado para corresponder a un `else` con el `if` más cercano que se encuentre alineado en su misma indentación.

# 6. ¿Cuál es la construcción para expresar múltiples selección que implementa C? ¿Trabaja de la misma manera que la de Pascal, ADA o Python?

La construcción de selección múltiple en C es el `switch`. Tiene el siguiente formato:
```c
    int a = 0;
    
    switch(a){ 
        case 0: printf("%d", a); break; // imprime 0
        case 1: printf("%s", "'a' es 1"); break;
        default: printf("%s", "'a' no es 0"); break;
    }
```
En este caso, va a buscar el `case` que coincida con el valor actual de 'a' y ejecuta el bloque de código. Si no coincide con ninguno, ejecuta el `default`.

Es necesario el uso de la instrucción `break` si no se quiere que se ejecute más de una opción, puesto que las condiciones se evalúan secuencialmente y puede haber casos en los que se cumplan varias; sin en este ejemplo no estuviese el `break` al terminar `case 0`, imprimiría tanto el valor de `a` como *" 'a' no es 0 "*. A esta característica se le llama *"fall-through automático"*.

En Pascal, la construcción para selección múltiple es el `case`. Funciona de manera similar al `switch` de C, pero no necesita instrucciones `break`. A diferencia del `default` de C que se ejecutaba siempre, el `else` de Pascal sólo se ejecuta si no se encuentra el valor buscado.

```pascal
begin
  a := 2;

  case a of
    1:
      writeln('"a" es 1');
    2:
      writeln('"a" es 2');
    3:
      writeln('"a" es 3');
    else
      writeln('Error');
  end;
end.
```

En Ada, la construcción para selección múltiple es el `case`. Funciona de manera similar al de Pascal:

```ada

    a: Integer := 2;

    case a is
        when 1 =>
        Ada.Text_IO.Put_Line("'a' es 1");
        when 2 =>
        Ada.Text_IO.Put_Line("'a' es 2");
        when 3 =>
        Ada.Text_IO.Put_Line("'a' es 3");
        when others =>
        Ada.Text_IO.Put_Line("Error");
    end case;
```

Hasta antes de la versión 3.10, Python no tenía una construcción de selección múltiple, pero podía usarse el bloque `elif` como alternativa a un `if` principal para crear una funcionalidad similar; también se podía usar el `else` normal para los casos en los que no se encontraban coincidencias.

A partir de la versión 3.11 de Python está la estructura de control `match case`, que funciona de manera similar al `case` de Pascal y Ada:
```python
a = 2;

match a:
    case 1:
        print("'a' es 1")
    case 2:
        print("'a' es 2")
    case 3:
        print("'a' es 3")
    case _:
        print("Error")
```
En esta estructura, el caso sin coincidencias se define como `case _`.

# 7. Sea el siguiente código:
```pascal
    var i, z:integer;

    Procedure A;
    begin
        i:= i +1;
    end;

begin
    z:=5;
    for i:=1..5 do begin
        z:=z*5;
        A;
        z:=z + i;
    end;
end;
```

## a. Analice en las versiones estándar de ADA y Pascal, si este código puede llegar a traer problemas. Justifique la respuesta.

En Ada, la ejecución de este código daría un error de compilación porque no se permite realizar asignaciones a variables que están siendo utilizadas para iterar sobre un loop `for`. Estas variables se consideran de sólo lectura.

En Pascal el código no traería problemas; el `for` se ejecutaría tres veces debido al incremento del índice dentro del bucle.

Las versiones estándar que encontré fueron **Pascal ISO 7185** y **Ada 2012**.

## b. Comente qué sucedería con las versiones de Pascal y ADA, que usted utilizó.

No lo hice así que no usé ninguna versión 🤩🤩

# 8. Sea el siguiente código en Pascal analice, si esto mismo, con la sintaxis correspondiente, puede trasladarse así a los lenguajes ADA y C. ¿Provocaría error en algún caso? Diga cómo debería hacerse en cada lenguaje y explique el por qué. Codifíquelo.

```pascal
program Main;

var puntos: integer;
begin
    puntos := 4;
    
    case puntos of
        1..5: write('No puede continuar');
        10: write('Trabajo terminado');
    end;
end.
```

En C no podría hacerse, puesto que no se permite usar un rango `1..5` como valor para entrar a un `case`. Sin embargo, se puede aprovechar el *fall-through automático* para hacer que varios valores ejecuten el mismo código, simulando el rango de Pascal:
```c
int main() {
    int puntos = 4;
    
    switch (puntos) {
        case 1:
        case 2:
        case 3:
        case 4:
        case 5:
            printf("No puede continuar");
            break;
        case 10:
            printf("Trabajo terminado");
            break;
    }
}
```

Ada sí permite el uso de rangos, al igual que Pascal; la única diferencia es que si no ponía el caso de `others` no me dejaba compilar. El código quedaría así:
```ada
    puntos : Integer := 4;
begin
   case puntos is
      when 1..5 =>
         Ada.Text_IO.Put_Line("No puede continuar");
      when 10 =>
         Ada.Text_IO.Put_Line("Trabajo terminado");
      when others =>
          Ada.Text_IO.Put_Line("Fuera de rango");
   end case;
```

# 9. Qué diferencia existe entre el generador `YIELD` de Python y el return de una función. De un ejemplo donde sería útil utilizarlo.

`yield` es una instrucción de Python que permite generar valores de manera iterativa. Cuando una función llega a una instrucción `yield`, retorna un valor y detiene su ejecución hasta que se la vuelva a llamar; cuando es invocada nuevamente, reanuda su ejecución desde la próxima instrucción.

La principal diferencia con el `return` es que al retornar de una función y al llamarla luego nuevamente, esta empieza siempre desde el principio.

Un ejemplo donde `yield` podría ser útil es para generar valores infinitamente, puesto que su ejecución se detiene pero va a continuar desde donde se quedó la próxima vez que se le llame; esto permite que genere valores nuevos constantemente.

# 10. Describa brevemente la instrucción `map` en JavaScript y sus alternativas.

`map` es una instrucción de JavaScript que permite crear un nuevo arreglo aplicándole una función a cada elemento de un arreglo ya existente. La instrucción no modifica al arreglo original, si no que retorna uno nuevo con las transformaciones de cada elemento; aunque puede asignarse al mismo arreglo para modificarse.

La sintaxis de un `map` es:
```javascript
let arr = [ 1, 2, 3, 4 ];
let arrNuevo = arr.map(a => a + 1);

console.log(arrNuevo); // imprime [ 2, 3, 4, 5 ]
```

Algunas alternativas para `map` son:
* `for..of`: recorre cada elemento de un arreglo. Con esta estructura pueden modificarse directamente los elementos del arreglo original, o agregarlos y modificarlos en un nuevo arreglo.
```javascript
let arr = [ 1, 2, 3, 4 ];
let arrNuevo = [];

for (let elem of arr) {
  arrNuevo.push(elem + 1);
}

console.log(arrNuevo); // imprime [ 2, 3, 4, 5 ]
```
* `forEach`: instrucción que realiza una función por cada elemento de un arreglo. A diferencia del `map` no retorna un arreglo nuevo, y a diferencia de `for..of` no puede modificar los valores del arreglo original; esta instrucción es útil para realizar operaciones con los valores, pero sin modificarlos.
```javascript
let arr = [ 1, 2, 3, 4 ];
let arrNuevo = [];

arr.forEach(a => arrNuevo.push(a + 1));

console.log(arrNuevo); // imprime [ 2, 3, 4, 5 ]
```
# 11. Determine si el lenguaje que utiliza frecuentemente implementa instrucciones para el manejo de espacio de nombres. Mencione brevemente qué significa este concepto y enuncie la forma en que su lenguaje lo implementa. Enuncie las características más importantes de este concepto en lenguajes como PHP o Python.

El espacio de nombres se utiliza para organizar y agrupar elementos del lenguaje (variables, funciones, etc.) dentro de un contexto, bajo un mismo nombre, para evitar conflictos con otros elementos del programa.

En JavaScript se usa el espacio de nombres a través de objetos, que agrupan variables y métodos relacionados.
```javascript
let objetoUno = {
    nombre: 'Cali',
    edad: 13,
    raza: 'Labrador Retriever',
    saludar: function() {
        console.log(`Hola, ${this.nombre}!`);
    }
}

let objetoDos = {
    nombre: 'Diva',
    edad: 5,
    raza: 'Jack Russell',
    saludar: function() {
        console.log(`Hola, ${this.nombre}!`);
    }
}
```
Se pueden acceder a las propiedades de un objeto directamente con la notación de punto (por ejemplo, `objetoUno.nombre`, `objetoDos.saludar()`), y aunque las propiedades de ambos objetos tengan los mismos nombres, al referenciarlas con esta notación no van a interferir entre sí.

Otra manera de organizar el espacio de nombres en JavaScript es a través de módulos, pero son muy largos así que no lo voy a ejemplificar.

Dentro de un módulo se trabajan con las variables internas, y las demás partes del programa sólo pueden utilizar los elementos que el módulo decida "exportar"; esto permite que el módulo pueda trabajar con sus propiedades internamente sin tener que preocuparse por colisiones de nombres con elementos de otros módulos.

* **PHP:** se utilizan *namespaces* para agrupar a los elementos relacionados. Luego para acceder a las propiedades de un *namespace* desde otra parte del programa se usa la palabra clave `use`.
* **Python:** también permite el uso de módulos. Estos se pueden importar luego en otros archivos usando la instrucción `from <módulo> import <elementos>`.