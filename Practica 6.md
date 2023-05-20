# 1. Explique brevemente los siguientes conceptos:

* **Parámetro:** variables usadas para enviar y recibir datos desde los subprogramas.
* **Parámetro real:** parámetro enviado al subprograma. Se define cuando se realiza la invocación y se corresponde con un parámetro formal.
* **Parámetro formal:** parámetro que se recibe y utiliza internamente en el subprograma. Está definido en el encabezado y su valor se corresponde con un parámetro real, dependiendo del tipo de ligadura usada.
* **Ligadura posicional:** los parámetros reales se asocian con un parámetro formal según el orden en el que fueron definidos.
* **Ligadura por nombre:** los parámetros reales se asocian con un parámetro formal asignándoles un nombre que indica con cuál deben ligarse.

# 2. Unir los siguientes puntos según corresponda y de una definición y un ejemplo de cada par.

| Modo | Tipo de parámetro | Definición |
| ---- | ----------------- | ---------- |
| OUT | Resultado | La ligadura se realiza sólo al final del subprograma; no se recibe ningún valor inicial, por lo que debe inicializarse internamente |
| IN | Valor | La ligadura se realiza sólo al inicio; el subprograma puede modificar el valor del parámetro y el programa que lo invocó nunca se va a dar cuenta. |
| IN/OUT | Valor-Resultado | Se realiza una ligadura al inicio y otra al final. El subprograma puede modificar el valor del parámetro, pero el programa que lo invocó sólo va a recibir el valor que tenga al final. |
| IN/OUT | Nombre | El parámetro formal recibe una expresión y un puntero de retorno hacia el argumento. La ligadura se realiza al inicio, pero se difiere hasta que sea necesario tomar el valor. |
| OUT | Resultado de funciones | El programa que invoca a la función espera un valor de retorno que sólo va a ser enviado cuando termine la ejecución de la función. |
| IN | Valor constante | Al ser un valor constante no pueden realizarse cambios sobre él, por lo que sólo va a realizar una ligadura inicial para obtener el valor. |
| IN/OUT | Referencia | Se envía como parámetro una referencia a una dirección de memoria, por lo que todos los valores modificados dentro del subprograma se verán inmediatamente reflejados en el programa que lo invocó. Se realiza una ligadura inicial que permanece hasta que termina el programa. |

# 3.

## a. Complete el siguiente cuadro según lo correspondiente a cada lenguaje:

| Tipo de pasaje de parámetros | Lenguaje |
| ---------------------------- | -------- |
| Valor, Constantes, Por nombre, Referencia | Ada |
| Valor, Referencia (punteros y arreglos) | C |
| Valor (copia del objeto en vez del original), Referencia (objetos mutables) | Ruby |
| Valor, Referencia (objetos) | Java |
| Valor, Referencia (objetos mutables) | Python |

## b. Ada es más seguro que Pascal respecto al pasaje de parámetros en las funciones. Explique por qué.

Ada es más seguro porque brinda más tipos de pasaje de parámetros, por lo que pueden realizarse distintas combinaciones más flexibles que en Pascal.

### c. Explique cómo maneja Ada los tipos de parámetros IN/OUT de acuerdo al tipo de dato.

Los tipos básicos (enteros, caracteres, etc.) se envían a través de valor/resultado; se envía una copia del valor al subprograma y no va a modificar al dato original hasta que termine de ejecutarse.

Los tipos compuestos (arrays, listas, etc.) se envían a través de referencias. Los cambios realizados en el parámetro del subprograma se ven inmediatamente en el dato original.

# 4. Sea el siguiente programa escrito en Pascal-like

```pascal
Procedure Main;
var
    j, m, i: integer;
    
    Procedure Recibe (x:integer; y:integer);
    begin
        m:= m + 1 + y;
        x:=i + x + j;
        y:=m - 1;
        write (x, y, i, j, m);
    end;

    Procedure Dos;
    var m:integer;
    begin
        m:= 5;
        Recibe(i, j);
        write (i, j, m);
    end;

begin
    m:= 2;
    i:=1; j:=3;
    Dos;
    write (i, j, m);
end.
```

## a. Arme el árbol de anidamiento sintáctico y el registro de activación de cada una de las unidades.

```
     Main
      |
 |---------|
 |         |
Recibe    Dos
```

| Main |
| ---- |
| PR |
| Current |
| Free |
| j; m; i; |
| Procedure recibe; Procedure dos |
| VR |

| Recibe |
| ------ |
| PR |
| LE: Main |
| LD: Dos |
|  x; y; |
| VR |

| Dos |
| --- |
| PR |
| LE: Main |
| LD: Main |
| m; |
| VR |

## b. Decir qué imprime el programa suponiendo que para todas las variables que se pasan el pasaje de parámetros es por:

### i. Referencia

<img src="./img/Practica 6/ej4referencia.png">

### ii. Valor

<img src="./img/Practica 6/ej4valor.png">

### iii. Valor-resultado

<img src="./img/Practica 6/ej4valor-resultado.png">

### iv. Nombre

<img src="./img/Practica 6/ej4nombre.png">

### v. Resultado

No se puede hacer por que el mecanismo de parámetros por resultado es de tipo OUT; esto implica que sólo se realiza una ligadura de valor a la salida, por lo que los parámetros nunca reciben un valor inicial.

Por cómo está diseñado el programa, los parámetros `x` e `y` esperan recibir un valor inicial para poder completar sus instrucciones, por lo que usar un tipo de parámetro de salida provocaría un error.

## c. ¿Existió algún caso que no pudo realizarlo porque saltó algún tipo de error? Diga cuál y por qué.

El parámetro por Resultado y ya lo expliqué arriba 😴

## d. ¿Dará el mismo resultado si se trata de un lenguaje que sigue la cadena dinámica? Justifique la respuesta realizando las pilas de activación

El único cambio que se realiza al seguir la cadena dinámica es el valor del dato `m`, puesto que es un identificador tanto del Main como el procedimiento Dos.

El error de los parámetros por salida se seguiría dando.

# 5. Suponiendo que se está ejecutando un programa con el siguiente registro de activación en memoria y se llama al procedimiento rutina(iter,vec,a). Determine el tipo de parámetro que se deben utilizar en el llamado para que los resultados sean los siguientes:

```c
// ...
procedura rutina(tipoParam iteracion,tipoParam vector,tipoParam vit):
    while iteracion begin
        vit = a+1
        vector[vit] = vector[vit]+1
        iteracion = (vector[vit] mod 2)==0
    end;
    print vec
    print vector
    print vit
    print a
// ...
rutina(iter,vec,a)
```

| PR |
| -- |
| LD |
| LE |
| iteracion = true; |
| vec = [ 3, 5, 6 ] |
| a = -1; |
| Rutina() |
| VR |

* `(4,6,7),(4,6,7), 2, 2`:  `vec` y `a` de entrada-salida.
* `(3,5,6),(4,6,7), 2, 2`: `vec` de entrada y `a` de entrada-salida.
* `(3,5,6),(5,5,6), 0, -1`: `vec` de entrada-salida y `a` de entrada. Siempre modifica `vec[0]` puesto que `a` nunca cambia.

# 6. Indique con un ejemplo el comportamiento del parámetro por nombre (en el parámetro formal) para los siguientes casos de parámetros reales:

No voy a dar un ejemplo pero más o menos los voy a explicar

###  Un valor entero

Funciona de manera igual que un parámetro por referencia; los cambios en el parámetro formal se realizan inmediatamente en el parámetro real.

En la ligadura del valor recibe una expresión y un puntero hacia el parámetro real.

### Una constante.

En la ligadura de valor recibe una expresión y el puntero hacia la constante. Lo que contiene realmente es una referencia a la constante, pero como estas no pueden ser modificadas funciona igual que un parámetro de entrada.

### Un elemento de un arreglo.

En cada cambio sobre el parámetro se vuelve a comprobar la expresión recibida, por lo que si cambia el índice sobre el que se trabaja puede cambiar el elemento del arreglo.

Con este sí voy a dejar un ejemplo porque no se entiende:
```c
var
    i: integer;
    arr: array[1..10] of integer;

    procedure uno(nombre elem: integer)
    begin
        elem := 2; // modifica array[1]
        i := i + 1;
        elem := 4; // modifica array[2]
    end;
begin
    i := 1;
    uno(array[i]);
end.
```
Cada vez que se cambia `elem` se vuelve a comprobar lo que haya en `array[i]`. Como el procedimiento cambia el valor de `i`, el elemento al que se referencia en cada cambio es diferente.

### Una expresión.

Al igual que con el elemento de un arreglo, las expresiones se vuelven a evaluar en el momento que son utilizadas; los valores podrían cambiar desde que se invoca al subprograma hasta que se usa el parámetro.

# 7. Realice la pila de ejecución del siguiente programa siguiendo la cadena estática y dinámica

```pascal
Procedure Uno;
y, z: integer;
r1:array[1..6] of integer;
r2:array[1..5] of integer;

Procedure Dos(nombre x, t:integer; var io:integer; valor-resultado y:integer);

    Procedure Dos(nombre t1: integer);

        Procedure Tres;
        begin
            y:= y + 1;
            z:= z + 1;
        end;
        
    begin
        t1:= t1 + 1;
        t:= t + 1;
        Tres;
        t1:= t1 + 2;
        t:= t + 2;
    end;

begin
    x:= x + 1;
    t:= t + 1;
    io:= io + 1;
    x:= x + 2;
    if z =2 then Dos(t);
end;

begin
    for y:= 1 to 6 do r1(y):= 2;
    for y:= 1 to 5 do r2(y):= 1;
    z:= 2;
    y:= 1;
    Dos( r1( y + r2( y )), r2( z ), y, z);
    for y:= 1 to 6 do write (r1(y));
    for y:= 1 to 5 do write (r2(y));
end.
```

<img src="./img/Practica 6/ej7estatica.png">

Las cadenas estáticas y dinámicas son iguales 🤝