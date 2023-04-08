# 1. ¿Qué define la semántica?

La semántica es el conjunto de reglas que le da significado a los programas sintácticamente válidos. A partir de la sintaxis, la semántica define qué hacer con lo escrito.

# 2.
### a. ¿Qué significa compilar un programa?

Compilar un programa significa ejecutar un programa compilador encargado de analizar el código original para que sea válido, y generar un código nuevo para ejecutar el programa traduciendo el código a lenguaje de máquina. La compilación se realiza siempre **antes** de la ejecución del programa.

El código original se llama “código fuente”, mientras que el código una vez compilado se llama “código objeto”.

### b. Describa brevemente cada uno de los pasos necesarios para compilar un programa.

La compilación se divide en dos etapas:

1. Etapa de análisis: vinculada a características del código fuente.
    1. Análisis léxico: divide los elementos del programa (identificadores, delimitadores, símbolos, etc.) y analiza que el código sea válido según las reglas del lenguaje.
    2. Análisis sintáctico: identifica las estructuras del código. Esta etapa se alterna con el análisis léxico y el semántico.
    3. Análisis semántico: procesa las estructuras sintáctica reconocidas para darle forma al código ejecutable.
    
Al terminar esta etapa se crea un código intermedio, que es parte del código objeto pero aún es dependiente a la máquina sobre la que se ejecuta.
    
2. Etapa de síntesis: vinculado a características del código objeto, al Hardware y a la arquitectura donde se ejecuta.
    1. Generación del código objeto
    2. Optimización de código (opcional)

### c. ¿En qué paso interviene la semántica y cual es su importancia dentro de la compilación?

La semántica interviene en el análisis semántico de la compilación, que es donde se procesa la sintáxis para darle el significado el código ejecutable.

# 3. Con respecto al punto anterior ¿es lo mismo compilar un programa que interpretarlo? Justifique su respuesta mostrando las diferencias básicas, ventajas y desventajas de cada uno.

Las diferencias entre compilar un programa y interpretarlo son:
| - | Intérprete | Compilador |
| - | ---------- | ---------- |
| **Ejecución**| Se ejecuta a la vez que se ejecuta el programa. | Se ejecuta antes que el código, para producir un código objeto. |
| **Orden** | Sigue el orden lógico de las instrucciones, y sólo analiza las que realice el programa. | Sigue el órden físico de las sentencias y ejecuta todas las instrucciones. |
| **Eficiencia** | Es más lento, porque el intérprete se repite cada vez que se ejecuta el programa. |  Es más rápido porque se compila una sola vez, y luego se ejecuta el programa en código objeto. |
| **Detección de errores** | Se pueden detectar las sentencias exactas en las que ocurrió el error. | Las referencias al código fuente se pierden en el código objeto; esto incluye las referencias a sentencias con errores. |

# 4. Explique claramente la diferencia entre un error sintáctico y uno semántico. Ejemplifique cada caso.

Los errores sintácticos son aquellos que se dan debido a un error en la gramática del lenguaje. El ejemplo más claro es el de escribir mal la definición de alguna estructura de control:
```java
    for (int i=0;i < 10){
        ///...
    }
```
En este caso, a esta estructura for le falta la expresión para incrementar i (normalmente `i++`), por lo que se detecta el error sintáctico y no se puede ejecutar.

Los errores semánticos son aquellos que, a pesar de ser sintácticamente correctos, dan un resultado no deseado o generan un error. Un ejemplo podría ser una división por 0; aunque esté bien definida sintácticamente, va a producir un error en el programa puesto que es matemáticamente imposible.

# 5. Sean los siguientes ejemplos de programas. Analice y diga qué tipo de error se produce (Semántico o Sintáctico) y en qué momento se detectan dichos errores (Compilación o Ejecución). Aclaración: Los valores de la ayuda pueden ser mayores.

## a.
```pascal
Program P
    var 5: integer;
    var a: char;
Begin
    for i:=5 to 10 do begin
        write(a);
        a=a+1;
    end;
End.
```

1. Los nombres de las variables no pueden ser números (*sintáctico*).
2. Para asignar el valor a una variable se debe usar `:=` (*sintáctico*).
3. La variable `a` está declarada pero nunca se inicializa (*semántico*).
4. La variable `i` no está declarada en el programa (*semántico*).
5. No se puede sumar a una variable de tipo `char` (*semántico*).

## b.
```java
public String tabla(int numero, arrayList<Boolean> listado) {
    String result = null;
    for(i = 1; i < 11; i--) {
    result += numero + "x" + i + "=" + (i*numero) + "\n";
    listado.get(listado.size()-1)=(BOOLEAN) numero>i;
}
    return true;
}
```

1. Cuando realiza el casteo a (BOOLEAN), debería estar en minúscula (*sintáctico*).
2. Se está intentando usar el método `get` y el operador `=` para almacenar un valor en una lista, pero esto se realiza con el método `set` (*sintáctico*).
3. Intenta realizar una suma en `result`, pero como la variable es tipo String va a terminar concatenando (*semántico*).
4. Si la variable `i` no está declarada en el programa (*semántico*).
5. Se está intentando usar un boolean para obtener un valor, siendo que la función `get` recibe sólo un integer (*semántico*).
6. El encabezado de la función dice que devuelve un String, pero intenta devolver un boolean (*semántico*).
7. Si se inicializa un String en null y se intenta operar con él, va a producir una excepción NullPointerException (*lógico*).

## c.
```c
# include <stdio.h>
int suma; /* Esta es una variable global */
int main()
{
    int indice;
    encabezado;
    for (indice = 1 ; indice <= 7 ; indice ++)
    cuadrado (indice);
    final(); Llama a la función final */
    return 0;
}
cuadrado (numero)
int numero;
{
    int numero_cuadrado;
    numero_cuadrado == numero * numero;
    suma += numero_cuadrado;
    printf("El cuadrado de %d es %d\n",
    numero, numero_cuadrado);
}
```

1. Nunca se define el tipo de la variable `encabezado` (*sintáctico*).
2. El comentario que está cuando se llama a `final()` no tiene el `/*` inicial, por lo que no lo reconoce como comentario (*sintáctico*).
3. El `for` no tiene las llaves, por lo que nunca se sabe cuando empieza y cuando termina (*sintáctico*).
4. El llamado a la función `cuadrado` está fuera de los corchetes de `main`(*semántico*).
5. La función `cuadrado` no está declarada; sólo se ven sus parámetros (*semántico*).
6. La función `final` no está declarada pero igualmente se la llama (*semántico*).
7. Se usa el operador `==` para realizar una asignación, cuando tendría que ser `=` (*semántico*).

## d.
```python
#!/usr/bin/python
print "\nDEFINICION DE NUMEROS PRIMOS"
r = 1

while r = True:
    N = input("\nDame el numero a analizar: ")
    i = 3
    fact = 0
    if (N mod 2 == 0) and (N != 2):
        print "\nEl numero %d NO es primo\n" % N
    else:
        while i <= (N^0.5):
            if (N % i) == 0:
                mensaje="\nEl numero ingresado NO es primo\n" % N
                msg = mensaje[4:6]
                print msg
                fact = 1
            i+=2
        if fact == 0:
            print "\nEl numero %d SI es primo\n" % N

    r = input("Consultar otro número? SI (1) o NO (0)--->> ")
```
1. Los `print` no tienen los paréntesis (*sintáctico*).
2. El operador para calcular el módulo en Python es `%`, pero usa la condición `N mod 2 == 0` en el if (*sintáctico*).
3. El `while r = True` está usando un solo = para hacer una comparación; debería ser `==` (*semántico*).
4. Como N lo recibe por input, por defecto es de tipo String. Sin embargo, aún se intentan hacer ciertas operaciones usándolo como número (*semántico*).
5. El operador `^` en Python se usa para comparar bytes, pero acá se usa como si fuese para hacer potencias (*semántico*).
6. Al terminar el While, el valor de R va a cambiar por un Input, así que pasa a ser un String. Si bien Python puede convertir un 1 a un boolean en True, no puede hacer lo mismo con una cadena de texto (*semántico*).

## e.

**Odio** ruby así que no lo voy a hacer 👍

# 5. Dado el siguiente código escrito en pascal. Transcriba la misma funcionalidad de acuerdo al lenguaje que haya cursado en años anteriores. Defina brevemente la sintaxis (sin hacer la gramática) y semántica para la utilización de arreglos y estructuras de control del ejemplo.

Lo único que entendí es que hay que escribirlo en otro lenguaje 😴

```pascal
Procedure ordenar_arreglo(var arreglo: arreglo_de_caracteres;cont:integer);
var
    i:integer; ordenado:boolean;
    aux:char;
begin
    repeat
        ordenado:=true;
        for i:=1 to cont-1 do
            if ord(arreglo[i])>ord(arreglo[i+1])
            then begin
                aux:=arreglo[i];
                arreglo[i]:=arreglo[i+1];
                arreglo[i+1]:=aux; ordenado:=false
            end;
    until ordenado;
end;
```
#### JavaScript
```javascript
arreglo.sort((a,b) => a - b);
```

# 6. Explique cuál es la semántica para las variables predefinidas en lenguaje Ruby self y nil. ¿Qué valor toman? ¿Cómo son usadas por el lenguaje?

`self` es una palabra usada en las estructuras de clases para indicar que un objeto está refiriéndose a sí mismo. Se usa para acceder a las variables propias de un objeto, o para usar su comportamiento independientemente de dónde se llame en la jerarquía (por ejemplo, si se llama en el método de una superclase). El valor que toma es la referencia al objeto actual.

`nil` es una palabra que indica que un objeto no tiene una referencia de memoria definida. Puede usarse para declarar objetos sin instanciarlos, o para retornar valores vacíos de un método.

# 7. Determine la semántica de null y undefined para valores en javascript.¿Qué diferencia hay entre ellos?

`null` en JavaScript tiene una función similar a `nil` en Ruby. Indica que un objeto no tiene una referencia en memoria definida. Dentro del lenguaje, `null` funciona como un objeto el cual no tiene ningún valor.

`undefined` indica que un campo no tiene un valor definido, pero que dicho campo está declarado. Dentro del lenguaje, `undefined` es un tipo de valor primitivo.

La diferencia principal entre ambos es que `null` generalmente es un valor asignado por el programador, mientras que `undefined` está asignado por el lenguaje en casos concretos (por ejemplo, cuando se inicializa una variable pero no se le asigna un valor).

# 8. Determine la semántica de la sentencia break en C, PHP, javascript y Ruby. Cite las características más importantes de esta sentencia para cada lenguaje.

En todos los lenguajes mencionados, la sentencia `break` sirve para interrumpir un bucle forzadamente. Sin embargo, tiene algunas diferencias en cómo funciona:
* En C, PHP y JavaScript, si está en un bucle anidado, sólo interrumpe la repetición del bucle en el que se encuentra la sentencia.
* En Ruby, la sentencia puede usarse además para salir de un bloque entero de código. También tiene la opción de retornar un valor.

# 9. Defina el concepto de ligadura y su importancia respecto de la semántica de un programa. ¿Qué diferencias hay entre ligadura estática y dinámica? Cite ejemplos (proponer casos sencillos)

La ligadura consiste en la asociación de una entidad con el atributo que la representa dentro de un lenguaje. Este concepto permite a la semántica saber el valor, tipo y lugar en memoria de las variables, por lo que es importante para detectar errores de tipos u operaciones.

Las entidades pueden ser tanto variables como funciones o sentencias de código.

Las ligaduras pueden dividirse en:
* `Estáticas:` se establecen antes de la ejecución y no pueden modificarse mientras se está ejecutando.
* `Dinámicas:` se establecen durante el tiempo de ejecución y pueden modificarse siguiendo las reglas del lenguaje.

Un ejemplo de ligadura estática puede verse en un lenguaje como Pascal:
```pascal
program ligaduraEstatica;
var
    num1, num2: integer;
begin
  num1 := 10;
  num2 := 10 * num1;
  writeln(num2);
end.
```
En este programa se usa la ligadura para poder obtener el valor de `num1` y usarlo en la asignación de `num2`. Esta asignación es estática porque el tipo de ambas variables ya está definido desde antes de la ejecución; si el tipo de `num1` fuese un String, por ejemplo, la operación de asignación a `num2` daría un error de compilación puesto que a través de la ligadura ya se sabría que no puede realizarse una operación de multiplicación con una variable de tipo String.

Un ejemplo de ligadura dinámica puede verse en un lenguaje como JavaScript:
```javascript
let num1 = 10;
console.log(num1 * 10); // Output: 100

num1 = "Hola"; // Cambia el tipo de la variable dinámicamente
console.log(num1 * 10); // Output: NaN

num1 = "10"; 
console.log(num1 * 10); // Output: 100
```
En este programa se usa la ligadura para asignarle un valor a `num1`, que como le asignamos un número va a tener el tipo `number`. Al realizar el console.log vamos a poder ver el resultado de la operación correctamente.

Cuando se cambia el valor a un String, la ligadura cambia y su tipo pasa a ser `string`. Cuando intenta realizar la multiplicación, va a intentar convertir el String a un número; por esto vemos que en el primer caso retorna `NaN` y en segundo retorna el mismo resultado que la operación numérica.

La ligadura dinámica permite mayor flexibilidad en el programa al trabajar con varios tipos, pero puede dar lugar a errores como el caso del `NaN`.