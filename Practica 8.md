# 1. ¿Explique claramente a qué se denomina excepción?

Una excepción es una situación anómala que se produce durante la ejecución del programa, y que es imposible controlarla en el contexto actual.

Se supone que ocurren con poca frecuencia, pero deben establecerse mecanismos para controlarlas cuando aparezcan.

# 2. ¿Qué debería proveer un lenguaje para el manejo de las excepciones? ¿Todos los lenguajes lo proveen?

Un lenguaje que pueda controlar excepciones debe tener:
* Un modo de definirlas
* Un modo de lanzarlas y capturarlas
* Mecanismos para manejarlas una vez que son capturarlas
* Criterios para continuar la ejecución del sistema luego de capturarlas
* Herramientas para que el desarrollador pueda generar excepciones voluntariamente desde el código

No todos los lenguajes proveen mecanismos para manejar las excepciones, particularmente los lenguajes más antiguos o de bajo nivel. Por ejemplo, el lenguaje C no posee mecanismos de manejo de excepciones; sin embargo, lenguajes más modernos que extienden de él como C++ o C# sí implementaron estos mecanismos.

# 3. ¿Qué ocurre cuando un lenguaje no provee manejo de excepciones? ¿Se podría simular? Explique cómo lo haría

Generalmente, los lenguajes sin manejo de excepciones terminan automáticamente su ejecución al terminar un error e informan un mensaje.

La manera más efectiva de simular el manejo de excepciones es usando bloques `if-else`, en los que se valida una condición que produciría una excepción y definimos en los bloques alternativos los pasos a seguir en caso de que se produzca o no.

# 4. Cuando se termina de manejar la excepción, la acción que se toma luego es importante. Indique

## a. ¿Qué modelos diferentes existen en este aspecto?

* **Reasunción:** cuando se detecta una excepción, se la atiende y luego continúa el flujo normal del programa, a partir de la siguiente línea a donde se encontró la excepción. Este modelo es usado, por ejemplo, en PL/1.

* **Terminación:** cuando se detecta una excepción, se la atiende y se termina el bloque de código donde se produjo. Luego, el programa va a intentar continuar el flujo desde algún punto de retorno establecido o simplemente terminará toda la ejecución. Este modelo es usado, por ejemplo, en Java y Python.

## b. Dé ejemplos de lenguajes que utilizan cada uno de los modelos presentados anteriormente. Por cada uno responda respecto de la forma en que trabaja las excepciones.

PL/1:
* Modelo de terminación.
* Las excepciones se definen explícitamente con la instrucción `ON CONDITION <nombre_excepción>`, junto con su manejador. También hay excepciones ya definidas por el lenguaje, junto con sus manejadores.
* Se lanzan explícitamente con la instrucción `SIGNAL CONDITION <nombre_excepción>`.
* Cuando se crea un manejador, se lo apila en una pila de manejadores; cuando se lanza una excepción, se busca el último manejador creado para esa excepción en la pila, y se ejecuta el primero que se encuentre. Cada excepción se liga dinámicamente al último manejador que se creó para que la atienda.
* El alcance del manejador ocupa todo el bloque en el que fue declarado.
* La ejecución continúa en la próxima línea de donde se lanzó la excepción.

Java:
* Modelo de terminación.
* Las excepciones se definen como objetos que extienden de la clase `Exception`; hay excepciones ya definidas por el lenguaje, y el usuario puede crear nuevas.
* Se lanzan explícitamente mediante la instrucción `throw`, o implícitamente cuando el lenguaje detecta un error en ejecución.
* Las excepciones se manejan en bloques `try-catch`: si el código ejecutado en `try` produce una excepción, se ejecuta la secuencia alternativa que se define en `catch`.
* Una vez tratada la excepción, termina la ejecución del método donde se produjo.
* Tiene Stack-trace dinámico (o *propagación dinámica*): si el método donde se produjo no trata la excepción, se propaga hacia el método que lo invocó, y así sucesivamente hasta que se trate o se llegue al programa principal sin ser tratada. Si un método puede producir una excepción pero no la trata localmente, se debe aclarar en el encabezado del método como `<método> throws Exception`.

## c. ¿Cuál de esos modelos es más inseguro y por qué?

El modelo de reasunción se considera más inseguro porque al continuar la ejecución se pueden propagar errores que no hayan sido tratados correctamente en los manejadores. En el modelo de terminación, al interrumpir el flujo normal de ejecución ante un error, se puede mantener mejor la consistencia del programa.

# 5. La propagación de los errores, cuando no se encuentra ningún manejador asociado, no se implementa igual en todos los lenguajes. Realice la comparación entre el modelo de Java, Python y PL/1, respecto a este tema. Defina la forma en que se implementa en un lenguaje conocido por usted.

* **Java:** se termina por completo la ejecución del programa y se informa en consola la excepción no controlada junto con su Stack-trace. En el Stack-trace se muestran todos los llamados a métodos realizados hasta que se produjo la excepción.
* **Python:** se termina por completo la ejecución del programa y se informa en consola la excepción no controlada. Junto con la excepción se muestra un *traceback*, que a diferencia del Stack-trace de Java, muestra información más precisa sobre dónde ocurrió la excepción, como archivos o líneas de código.
* **PL/1:** se termina por completo la ejecución del programa y se genera un diagnóstico para debugging.

# 6. Sea el siguiente programa escrito en Pascal ¿Qué modelo de manejo de excepciones está simulando? ¿Qué necesitaría el programa para que encuadre con los lenguajes que no utilizan este modelo? Justifique la respuesta.
```pascal
Procedure Manejador;
Begin
    // ...
end;

Procedure P(X:Proc);
    begin
    // ...
    if Error then X;
    // ...
end;

Procedure A;
begin
    // ...
    P(Manejador);
    // ...
end;
```

Está simulando un modelo de reasunción, puesto que si encuentra un error va a invocar al procediminento `Manejador`, pero al terminar de ejecutarlo va a continuar desde la siguiente línea a donde fue llamado.

Para simular un modelo por terminación podrían hacerse dos cosas:
1. Que en el procedimiento `P` sólo se realice el `if`, y que no haya más código después; esto simularía tanto una reasunción como una terminación, puesto que el bloque donde se produce el error termina.
2. Usar una sentencia `return` en caso de que se encuentre el error; esto terminaría abruptamente la ejecución del procedimiento `P`, que es donde se generó el error.

# 7.  Sea el siguiente programa escrito en Pascal:

```pascal
Program Principal;
    var x:int; b1,b2:boolean;

    Procedure P (b1:boolean);
        var x:int;

        Procedure Manejador1
        begin
            x:=x + 1;
        end;
    begin
        x:=1;
        if b1=true then Manejador1;
        x:=x+4;
    end;

    Procedure Manejador2;
    begin
        x:=x * 100;
    end;

Begin
    x:=4;
    b2:=true;
    b1:=false;
    if b1=false then Manejador2;
    P(b);
    write (x);
End.

```
## a. Implemente este ejercicio en PL/1 utilizando manejo de excepciones

```ada
Prog Principal
    DECLARE x INTEGER;
    DECLARE b1 BOOLEAN;
    DECLARE b2 BOOLEAN;

    PROC P (b1 BOOLEAN)
        DECLARE x INTEGER;
    begin
        
        ON CONDITION Manejador1 begin
            x = x+1;
        end;

        x = 1;

        if (b1 = true) then
            SIGNAL CONDITION Manejador1;
        end;

        x = x+4;
    end;

begin

    ON CONDITION Manejador2 begin
        x = x*100;
    end;

    x = 4;
    b2 = true;
    b1 = false;

    if (b1 = false) then
        SIGNAL CONDITION Manejador2;
    end;

    CALL P(b1);
    WRITE(x);
end;
```

## b. ¿Podría implementarlo en JAVA utilizando manejo de excepciones? En caso afirmativo, realícelo.

Podría implementarse, pero el problema es que habría partes del código que no se ejecutarían. Por ejemplo, en el proceso `P` después de lanzar y tratar la excepción `Manejador1` ejecuta la instrucción `x = x+4`; esto no podría hacerse porque Java usa un modelo por terminación, a diferencia de PL/1.

Para implementarlo hay dos maneras posibles:
* Llamar a un método que ejecute el código con la posible excepción, que la atienda y sea terminado. Luego el flujo vuelve al método que la invocó, y puede continuar su ejecución.
* Usar el bloque `finally` junto con el `try-catch`; este bloque ejecuta el código independientemente de que el error haya ocurrido o no, luego de que se haya ejecutado el `try` o el `catch` según corresponda.

Lo voy a hacer con un `finally` porque hay que escribir menos código:
```java
public class Main
{
    
    public static void P(boolean b1){
        int x = 1;
        
        try {
            if (b1) throw new Manejador1();
        }
        catch(Manejador1 m1) {
            x += 1;
        }
        finally {
            x += 4;
        }
    }
    
	public static void main(String[] args) {
	    int x;
        boolean b1, b2;
	    
	    x = 4;
	    b1 = true;
	    b2 = false;
	    
	    try {
	        if (!b1) throw new Manejador2(); 
	    }
	    catch (Manejador2 m2) {
	        x*= 100;
	    }
	    finally {
	        P(b1);
		    System.out.println(x);
	    }
	}
}
```

# 8.  Sean los siguientes procedimientos de un programa escrito en Java:
```java
public class Main {
    
    public static void main (String[] argos){
        
        double array_doubles[]= new double[500];
        
        for (int i=0; i<500; i++){
            array_doubles[i]=7*i;
        }
        for (int i=0 ; i<600 ; i=i+25){
            try{
                System.out.println("El elemento en "+ i + " es " + acceso_por_indice (array_doubles,i));
            }
            catch(ArrayIndexOutOfBoundsException e){
                System.out.println(e.toString());
            }
            catch(Exception a){
                System.out.println(a.toString());
            }
            finally{
                System.out.println("sentencia finally");
            }
        }
    }
    
    public static double acceso_por_indice (double [] v, int indice) throws Exception,ArrayIndexOutOfBoundsException {
        if ((indice>=0) && (indice<v.length)){
            return v[indice];
        }
        else{
            if (indice<0){
                // caso excepcional
                throw new ArrayIndexOutOfBoundsException("el índice" + indice + " es un número negativo");
            } else{
                // caso excepcional
                throw new Exception(" el indice " + indice + " no es una posición válida");
            }
        }
    }
}
```

## a. Analizar el ejemplo y decir qué manejadores ejecuta y en qué valores quedan las variables. Justifique la respuesta.

Se lanzan dos excepciones:
* `ArrayIndexOutOfBounds`: excepción predefinida por el lenguaje. Se lanza cuando se intenta acceder a una posición que está fuera del tamaño de un array.
* `Exception`: excepción genérica predefinida por el lenguaje. Es la clase base de la que heredan todas las demás excepciones.

Como manejador se usa el código definido en el bloque `catch`. Lo que hace es imprimir el mensaje de error con el que son lanzadas las excepciones.

```c
El elemento en 0 es 0.0
sentencia finally
El elemento en 25 es 175.0
sentencia finally
El elemento en 50 es 350.0
sentencia finally
// ...
El elemento en 475 es 3325.0
sentencia finally
java.lang.Exception: el indice 500 no es una posición válida
sentencia finally
java.lang.Exception: el indice 525 no es una posición válida
sentencia finally
java.lang.Exception: el indice 550 no es una posición válida
sentencia finally
java.lang.Exception: el indice 575 no es una posición válida
sentencia finally
```
En este programa `ArrayIndexOutOfBounds` sólo se lanza cuando el índice es menor a 0 (que nunca pasa), por lo que todas las excepciones son de tipo `Exception`; normalmente Java también tira esa excepción cuando se supera el tamaño del array, pero como acá verificamos en el `if` que sólo sea menor a 0 no lo hace.

## b. La excepción se propaga o se maneja en el mismo método? ¿Qué instrucción se agrega para poder propagarla y que lleve información?

La excepción se propaga hacia el método `main`. Para propagarla hay que agregar dos cosas:
* `throws Exception, ArrayIndexOutOfBoundsException` en el encabezado del método.
* `throw new ArrayIndexOutOfBoundsException(<mensaje>)` y `throw new Exception(<mensaje>)` en el momento que se desea lanzar la excepción. En el mensaje se escribe la información que se quiere enviar; esta se recibe dentro del objeto que crea la excepción.

## c. ¿Cómo modificaría el método `acceso_por_indice` para que maneje él mismo la excepción?

```java
public static double acceso_por_indice (double [] v, int indice) throws Exception,ArrayIndexOutOfBoundsException {

    try {
        if (indice<0){
            throw new ArrayIndexOutOfBoundsException("el índice" + indice + " es un número negativo");
        } else if (indice > v.length) {
            throw new Exception(" el indice " + indice + " no es una posición válida");
        } else return v[indice];
    }
    catch (ArrayIndexOutOfBoundsException e){
        System.out.println(e.toString());
    } catch(Exception a){
        System.out.println(a.toString());
    } finally{
        System.out.println("sentencia finally");
    }
}
```

# 9. Indique diferencias y similitudes entre Phyton y Java con respecto al manejo de excepciones.

Similitudes:
* Ambos lenguajes usan un bloque del estilo `try-catch` para el manejo de excepciones. La única diferencia es que Python usa la palabra clave `except` en vez de `catch`, pero su funcionamiento es el mismo.
* Ambos lenguajes permiten el uso del bloque `finally` para ejecutar sentencias independientemente de que el código genere una excepción o no.
* Ambos lenguajes permiten lanzar excepciones explícitamente con la palabra clave `throw`.
* Ambos lenguajes permiten definir jerarquías de excepciones.

Diferencias:
* En Java debe declararse explícitamente qué excepciones puede lanzar un método, o atraparlas en un bloque `catch`. En Python esto puede evitarse.
* En Python todas las excepciones usando un bloque genérico `except`. En Java, se debe definir explícitamente el tipo de excepción que corresponde a cada `catch`, o usar un bloque que atrape excepciones de tipo `Exception`.
* Python no hace diferencias entre las excepciones declaradas en el método y las que lanza el lenguaje por defecto. Java sólo va a atender las excepciones que se haya declarado explícitamente que deben ser atrapadas.

# 10. ¿Qué modelo de excepciones implementa Ruby? ¿Qué instrucciones específicas provee el lenguaje para manejo de excepciones y cómo se comportan cada una de ellas?

Ruby maneja las excepciones usando un bloque `rescue-ensure-else`, que tiene algunas similitudes con el `try-catch` de Java.

1. El módulo comienza a ejecutarse normalmente (después de un `begin`)
2. Cuando detecta una excepción salta automáticamente al bloque `rescue` que pueda atrapar excepciones de ese tipo.
3. Si no se encuentra ninguna excepción, antes de terminar el módulo se ejecuta el bloque `else`.
4. Independientemente de que haya atrapado o no una excepción, se ejecuta el bloque `ensure` al finalizar.

Para lanzar excepciones explícitamente se usa la instrucción `raise <tipo_excepcion>, "Mensaje"`.

La principal diferencia con el `try-catch` es que en Ruby se atrapan las excepciones lanzadas en el código del módulo antes de que se haya definido el `rescue`, mientras que en `try-catch` sólo se atrapan las que hayan sido lanzadas dentro del bloque `try`.

Ruby usa un modelo de reasunción, por lo que las instrucciones que estén después del bloque `rescue-ensure-else` se ejecutarán aunque se detecte una excepción.

# 11. Indique el mecanismo de excepciones de JavaScript.

El mecanismo de excepciones de JavaScript funciona de manera muy similar al de Python: las maneja con un bloque `try-catch-finally`, puede lanzarlas explícitamente con `throw` y permite la jerarquía de excepciones con la clase base `Error`.

JavaScript usa un modelo de reasunción, por lo que la función en la que se detecta el error se sigue ejecutando después del bloque `try-catch` aunque se haya encontrado un error.

# 12. Sea el siguiente programa escrito en Python, Indique el camino de ejecución.
```python
#!/usr/bin/env python
#calc.py
def dividir():
    x = a / b
    print (("Resultado"), (x))

while True:
    try:
        a = int(input("Ingresa el primer numero: \n"))
        b = int(input("Ingresa el segundo numero: \n"))
        dividir()
        break
    except ZeroDivisionError:
        print("No se permite dividir por cero")
    finally:
        print ("Vuelve a probar")
```
## a. Describa qué caminos ejecuta para diferentes valores de ingreso

El camino de ejecución cambia dependiendo el valor ingresado para `b`.

* **Si `b = 0`:** va a llamar a la función `dividir()` que va a realizar una división por 0; debido a esto, el lenguaje va a lanzar implícitamente una excepción `ZeroDivisionError` que es atrapada desde el lenguaje principal. El bloque except va a imprimir el mensaje `"No se permite dividir por cero"` y el bloque finally va a imprimir `"Vuelve a probar"`. Como el `break` está sólo dentro del bloque try, el bucle se va a repetir infinitamente hasta que se ingrese un valor de `b` distinto a 0.
* **Si `b != 0`:** va a llamar a la función `dividir()` que va a realizar una división válida y va a imprimir el resultado en pantalla. Luego va a ejecutar la próxima línea de donde fue invocada, que corresponde al `break` que sale del while True. Luego, el bloque finally va a imprimir `"Vuelve a probar"` (es mentira no vamos a volver a probar😭).

Salida con valores `a = 1; b = 0` y `a = 1; b = 1` en la segunda iteración:
```python
Ingresa el primer numero: 
1
Ingresa el segundo numero: 
0
No se permite dividir por cero

Vuelve a probar
Ingresa el primer numero: 
1
Ingresa el segundo numero: 
1
Resultado 1.0
Vuelve a probar
```

Salida con valores `a = 10; b = 2`:
```python
Ingresa el primer numero: 
10
Ingresa el segundo numero: 
2
Resultado 5.0
Vuelve a probar
```

## b. Agregar el uso de una excepción anónima

Para agregar una excepción anónima tenemos que agregar un bloque `except` que atrape excepciones genéricas; es decir, del tipo básico `Exception`.

```python
#!/usr/bin/env python
#calc.py
def dividir():
    x = a / b
    print (("Resultado"), (x))

while True:
    try:
        a = int(input("Ingresa el primer numero: \n"))
        b = int(input("Ingresa el segundo numero: \n"))
        dividir()
        break
    except ZeroDivisionError:
        print("No se permite dividir por cero")
    except Exception:
        print("Hubo un error")
    finally:
        print ("Vuelve a probar")
```
Una manera fácil de probar esto es ingresando un valor no numérico en alguno de los dos input; esto normalmente es un `ValueError`, pero como definimos la excepción anónima la va a atrapar igual. La salida es la siguiente:
```python
Ingresa el primer numero: 
"AMO CPLP"                                   
Hubo un error
Vuelve a probar

Ingresa el primer numero: 
1
Ingresa el segundo numero: 
10
Resultado 0.1
Vuelve a probar
```

# 13. Dado el programa escrito en Java:
```java
public class ExcepcionUno extends Exception {
    public ExcepcionUno(){
        super(); // constructor por defecto de Exception
    }

    public ExcepcionUno(String cadena){
        super(cadena); // constructor param. de Exception
    }
}


public class ExcepcionDos extends Exception {
    public ExcepcionDos(){
        super(); // constructor por defecto de Exception
    }
    public ExcepcionDos(String cadena) {
        super(cadena); // constructor param. de Exception
    }
}

public class ExcepcionTres extends Exception {
    public ExcepcionTres(){
        super(); // constructor por defecto de Exception
    }

    public ExcepcionTres(String cadena) {
        super(cadena); // constructor param. de Exception
    }
}
```

```java
public class Lanzadora {
    public void lanzaSiNegativo(int param) throws ExcepcionUno {
    if (param < 0)
        throw new ExcepcionUno("Numero negativo");
    }

    public void lanzaSimayor100(int param) throws ExcepcionDos {
        if (param >100 and param<125)
            throw new ExcepcionDos("Numero mayor100");
    }
    public void lanzaSimayor125(int param) throws ExcepcionTres {
        if (param >= 125)
            throw new ExcepcionTres("Numero mayor125");
    }
}
```

```java
import java.io.FileInputStream;
import java.io.IOException;
public class Excepciones {

    public static void main(String[] args) {
        // Para leer un fichero
        Lanzadora lanza = new Lanzadora();
        FileInputStream entrada = null;
        int leo;

        try {
            entrada = new FileInputStream("fich.txt");
            while ((leo = entrada.read()) != -1){
                if (leo < 0)
                    lanza.lanzaSiNegativo(leo);
                else if (leo > 100)
                    lanza.lanzaSimayor100(leo);
            }

            entrada.close();
            System.out.println("Todo fue bien");
        }
        catch (ExcepcionUno e) { // Personalizada
            System.out.println("Excepcion: " + e.getMessage());
        }
        catch (ExcepcionDos e) { // Personalizada
            System.out.println("Excepcion: " + e.getMessage());
        }
        catch (IOException e) { // Estándar
            System.out.println("Excepcion: " + e.getMessage());
        }
        finally {
        if (entrada != null)
            try {
                entrada.close(); // Siempre queda cerrado
            }
            catch (Exception e) {
                System.out.println("Excepcion: " + e.getMessage());
            }
        System.out.println("Fichero cerrado.");
        }
    }
}
```
## a. Indique cómo se ejecuta el código. Debe quedar en claro los caminos posibles de ejecución, cuales son los manejadores que se ejecutan y cómo se buscan los mismos y si en algún caso se produce algún error.

El programa lee líneas de un archivo de texto hasta llegar a una que tenga el valor -1.

Cuando itera sobre los valores leídos, revisa que no sean ni menores a 0 ni mayores a 100.
* Si es menor a 0, se llama al método del objeto `Lanzadora` que lanza una excepción de tipo `ExcepcionUno`.
* Si es mayor a 0, se llama al método del objeto `Lanzadora` que lanza una excepción de tipo `ExcepcionDos`.

Si se encuentra el valor -1 y no se lanzaron excepciones, se cierra el lector de archivos y se notifica en consola que todo salió bien.

El while se encuentra en una estructura `try-catch` que tiene definidos tres manejadores:
1. Uno para `ExcepcionUno`, que se lanza explícitamente en el código. Imprime el mensaje de error en consola.
2. Uno para `ExcepcionDos`, que se lanza explícitamente en el código. Imprime el mensaje de error en consola.
3. Uno para `IOException`, que es la excepción lanzada por el lenguaje cuando tiene problema de operaciones de E/S; en este caso, al leer el archivo. Imprime el mensaje de error en consola.

Cuando termina de iterar sobre las líneas, independientemente de si haya lanzado excepción o no, ejecuta el bloque `finally`, que revisa si la variable *entrada* quedó con el valor "null". Dentro del `if` hay un bloque *try-catch* para atrapar las posibles excepciones lanzada por la instrucción `close()`; el manejador atrapa excepciones genéricas e imprime el mensaje de error en consola.

# 14. Dado el siguiente código en Java indique todos los posibles caminos de resolución, de acuerdo a los números que vaya leyendo del archivo.

```java
class ExcepcionE1 extends Exception {
    public ExcepcionE1(){
        super(); // constructor por defecto de Exception
    }

    public ExcepcionE1(String cadena){
        super(cadena); // constructor param. de Exception
    }
}

class ExcepcionE2 extends Exception {
    Public ExcepcionE2(){
        super(); // constructor por defecto de Exception
    }

    Public ExcepcionE2(String cadena){
        super(cadena); // constructor param. de Exception
    }
}
```

```java
public class Evaluacion {
    void Evalua(int edad) throws ExcepcionE1, ExcepcionE2 {
    if (edad < 18)
        throw new ExcepcionE1("Es una persona menor de edad");
    else if (edad> 70)
        throw new ExcepcionE2("Es persona mayor de edad");
    }

    void Segmenta(int edad) throws ExcepcionE1, ExcepcionE2 {
        if (edad < 35)
            throw new ExcepcionE1("Es una persona joven");
    }
}
```

```java
class AnalisisEdadPoblacion{

    public static void main(String[] args){
        // Para leer un fichero
        Evaluacion Invoca = new Evaluacion();
        FileInputSt ream entrada = null;
        int leo;
        try{
            entrada = new FileInputStream("fich.txt");
            while ((leo = entrada.read()) != -1) {
                try {
                    if (leo<0) {
                        throw new ExcepcionE1("Edad inválida");
                    } else {
                        if (leo>120){
                            throw new ExcepcionE1("Edad inválida");
                        }
                    }
                    invoca.evalua (leo);
                    invoca.segmenta(leo);
                    System.out.println("Es persona adulta, Todo fue bien");
                } catch (ExcepcionE2 e){
                    System.out.println("Excepcion: " + e.getMessage());
                } catch (ExcepcionE1 e){
                    System.out.println("Excepcion: " + e.getMessage());
                }
            }
        } catch (FileNotFoundException e1) {
            System.out.println("No se encontró el archivo");
        } catch (IOException e) {
            System.out.println("Problema para leer los datos");
        }finally {
        if (entrada != null)
            try {
                entrada.close();
            } catch (Exception e) {
                System.out.println("Excepcion: " + e.getMessage());
            }
            System.out.println("Fichero cerrado.");
        }
    }
}
```
* Se abre el archivo *"fich.txt"*.
    * Si no se encontró el archivo, se lanza una excepción `FileNotFoundException`. El manejador de esta excepción imprime en pantalla *"No se encontró el archivo"* y termina la ejecución del programa.
* Se lee una línea de texto del archivo.
    * Si hay un problema en la operación de E/S, se lanza una excepción `IOException`. El manejador de esta excepción imprime en pantalla *"Problema para leer los datos"* y termina la ejecución del programa.
    * Si el número leído es distinto a -1, entra al while siguiente.
    * Si el número es -1, salta directamente al bloque `finally`.
* Entra al while
    * Si el número leído es menor a 0 o mayor a 120, se lanza explícitamente una excepción `ExcepcionE1`. El manejador de esta excepción imprime en pantalla *"Excepción: Edad inválida"* y termina la ejecución del programa.
    * Se invoca al método `Evalua` de la clase **Evaluación**, enviándole como parámetro el número leído
        * Si el número es menor a 18, se lanza una excepción `ExcepcionE1` que se propaga dinámicamente hacia el manejador del programa principal; esto termina la ejecución del método. El manejador imprime en pantalla *"Excepción: Es una persona menor de edad"* y termina la ejecución del programa principal.
        * Si el número es mayor a 70, se lanza una excepción `ExcepcionE2` que se propaga dinámicamente hacia el manejador del programa principal; esto termina la ejecución del método. El manejador imprime en pantalla *"Excepción: Es una persona mayor de edad"* y termina la ejecución del programa principal.
    * Se invoca al método `Segmenta` de la clase **Evaluación**, enviándole como parámetro el número leído
        * Si el número es menor a 35, se lanza una excepción `ExcepcionE1` que se propaga dinámicamente hacia el manejador del programa principal; esto termina la ejecución del método. El manejador imprime en pantalla *"Excepción: Es una persona joven"* y termina la ejecución del programa principal.
    * Se imprime en pantalla *"Es una persona adulta, todo fue bien"*.

Si detecta un error al leer el archivo o si sale sin errores del while, se ejecuta el bloque `finally`
* Se revisa si la variable `entrada` (donde se lee el archivo) es distinta a null.
    * Si es distinta a null, se realiza la operación de cierre del archivo.
        * Si hay un error al cerrar el archivo, se lanza una excepción. El manejador de las excepciones genéricas imprime en pantalla *"Excepción: "* junto con el mensaje de la excepción.
* Imprime en pantalla *"Fichero cerrado"*.