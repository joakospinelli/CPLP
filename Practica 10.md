# 1. Un programa en un lenguaje procedural es una secuencia de instrucciones o comandos que se van ejecutando y producen cambios en las celdas de memoria, a través de las sentencias de asignación. ¿Qué es un programa escrito en un lenguaje funcional? y ¿Qué rol cumple la computadora?

En un programa funcional, las sentencias de código se dividen en funciones que retornan un valor. El programa entero se trata como una función, que a su vez está compuesto por otras funciones.

La computadora se encarga de evaluar y ejecutar las funciones para obtener los resultados adecuados.

# 2. ¿Cómo se define el lugar donde se definen las funciones en un lenguaje funcional?

Las variables están definidas dentro de un "ámbito léxico". Este puede hallarse en el programa principal o dentro de otra función.

El ámbito léxico define el contexto de una función; una función tiene acceso a todas las variables y funciones definidas dentro de su ámbito.

# 3. ¿Cuál es el concepto de variables en los lenguajes funcionales?

Los programas funcionales también tienen variables básicas y derivadas. Las funciones deben tener siempre asociado un tipo (ya sea básico o derivado).

En los lenguajes funcionales, las variables no tienen efectos colaterales; esto quiere decir que sus valores no se transforman. Su funcionalidad se basa principalmente en asociar un valor a un nombre para facilitar las operaciones.

# 4. ¿Qué es una expresión en un lenguaje funcional? ¿Su valor de qué depende?

Las expresiones son el punto central de los lenguajes funcionales. Se basan en la idea de que *"una expresión es su valor"*; esto significa que el valor de una expresión depende únicamente de las sub-expresiones que la componen.

Las expresiones pueden estar compuestas por variables, pero estas siguen el concepto de una variable matemática. Los valores de entrada no se modifican, si no que se usan para producir los valores de salida.

La transparencia referencial es una propiedad de las expresiones, que implica que al llamar a una función con los mismos valores de entrada siempre va a retornar el mismo resultado.

# 5. ¿Cuál es la forma de evaluación que utilizan los lenguajes funcionales?

La evaluación se realiza a través de un proceso de reducción. Se evalúa expresión por expresión y se van obteniendo resultados periódicos, con los cuales se realiza otra expresión hasta obtener el resultado final.

Hay dos formas posibles de realizar la reducción:
* **Orden aplicativo:** siempre evalúa los argumentos, aunque no lo necesite.
* **Orden normal (lazy evaluation):** evita hacer más cálculos de los necesarios. Una expresión no se evalúa hasta que su valor se necesite.

# 6. ¿Un lenguaje funcional es fuertemente tipado? ¿Qué tipos existen? ¿Por qué?

Se considera que los lenguajes funcionales son fuertemente tipados porque al evaluar las expresiones depende totalmente de los valores de entrada, por lo que es necesario que haya tipos definidos para facilitar las reglas de evaluación y que no haya incompatibilidad de tipos.

Los tipos de datos pueden ser básicos o derivados (definidos por el usuario).

# 7. ¿Cómo definiría un programa escrito en POO?

Los programas escritos en POO están formados por un conjunto de objetos que se comunican entre sí para llegar a un resultado común.

Los objetos están definidos a partir de clases que definen su estado interno y su comportamiento. Cada objeto puede encapsular su propia información, de manera que abstrae a los demás sobre cómo realiza sus funciones, y simplemente retorna resultados finales.

Las clases permiten definir estructuras complejas de composición o herencia, a través de las cuales se puede relacionar el comportamiento de los objetos.

# 8. Diga cuáles son los elementos más importantes y hable sobre ellos en la programación orientada a objetos.

* **Estado interno:** el estado interno de un objeto es el valor que toman sus variables internas en un momento específico.
* **Comportamiento:** el comportamiento de un objeto está definido por los métodos que puede realizar. La ejecución de un método se resuelve a través de mensajes, que es lo que permite la comunicación entre distintos objetos.
* **Clase:** tipos definidos por el usuario que definen la estructura básica, el estado y el comportamiento para objetos de un mismo tipo.
* **Encapsulamiento:** propiedad de las clases que permiten que una instancia pueda ocultar cierta parte de su implementación a los demás objetos. Gracias a esto se puede decidir qué componentes de un objeto pueden ser accedidos y qué otros deben permanecer ocultos.

# 9. La posibilidad de ocultamiento y encapsulamiento para los objetos es el primer nivel de abstracción de la POO, ¿cuál es el segundo?

El segundo nivel de abstracción es la herencia.

La herencia permite que una clase "herede" el estado y el comportamiento de otra, teniendo acceso a todas sus variables internas y métodos. Esto permite generar estructuras complejas de clases, en las que una clase inferior puede reutilizar los componentes ya definidos en clases superiores.

# 10. ¿Qué tipos de herencias hay? Cuál usa Smalltalk y C++

* **Herencia simple:** una subclase puede heredar de una única clase padre.
* **Herencia múltiple:** una subclase puede tener varias clases padre de las cuales hereda.
* **Herencia multinivel:** una subclase puede heredar de una única clase padre, pero el padre puede ser una clase derivada que hereda de otra; de esta manera se puede elaborar una "cadena" de herencias, en la que en cada nivel se pueden agregar nuevos componentes.

C++ permite tanto herencia simple como múltiple. Smalltalk, por otro lado, sólo permite la herencia simple.

# 11. En el paradigma lógico ¿Qué representa una variable? ¿y las constantes?

En el paradigma lógico, las variables son elementos indeterminados cuyo valor puede representar a cualquier constante de su tipo. A diferencia de otros paradigmas, las variables no pueden ser modificadas una vez que se le asigna un valor; esto se debe a que su funcionalidad es la de definir las relaciones del sistema.

Las constantes representan valor específicos del sistema, y se usan para evaluar los términos. Representan elementos concretos del dominio.

# 12. ¿Cómo se escribe un programa en un lenguaje lógico?

Los programas están definidos por una serie de aserciones lógicas. Se puede obtener un resultado a partir de la evaluación de las distintas aserciones.

El programa está escrito como una secuencia de cláusulas, que pueden ser un hecho o una regla:
* **Hecho:** definen el conocimiento de un programa. Representan las relaciones "verdaderas" entre objetos.
* **Regla:** retornan una conclusión a partir de una condición dada. Tienen la forma `conclusión :- condición`; las condiciones se evalúan siguiendo los hechos ya definidos por el lenguaje.

# 13. Teniendo en cuenta el siguiente problema, se lee una variable entera por teclado y si es par se imprime “El valor ingresado es PAR” y si es impar imprime “El valor ingresado es impar”, implemente este ejemplo en cada uno de los paradigmas presentados en esta práctica.

Funcional (Haskell):
```haskell
main :: IO ()
main = do
  putStrLn "Ingrese un número entero:"
  input <- getLine
  let number = read input :: Int
  if even number
    then putStrLn "El valor ingresado es PAR"
    else putStrLn "El valor ingresado es impar"
```

Lógico (PROLOG):
```prolog
main :- 
  writeln('Ingrese un número entero:'),
  read(Number),
  checkParImpar(Number).

checkParImpar(Number) :-
  (Number mod 2 =:= 0 ->
    writeln('El valor ingresado es PAR')
  ;
    writeln('El valor ingresado es impar')
  ).
```

POO (Java):
```java
import java.util.Scanner;

public class ParImpar {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Ingrese un número entero:");
        int number = scanner.nextInt();

        NumeroEntero num = new NumeroEntero(number);

        if (num.esPar()) {
            System.out.println("El valor ingresado es PAR");
        } else {
            System.out.println("El valor ingresado es impar");
        }
    }
}

class NumeroEntero {
    private int numero;

    public NumeroEntero(int numero) {
        this.numero = numero;
    }

    public boolean esPar() {
        return numero % 2 == 0;
    }
}
```

Basado en Scripts (Python):
```python
numero = int(input("Ingrese un número: "))
print("El número es par") if (numero % 2 == 0) else print("El número es impar")
```

# 14. Describa las características más importantes de los Lenguajes Basados en Scripts. Mencione diferentes lenguajes que utilizan este concepto. ¿En general, qué tipificación utilizan?

Los lenguajes basados en Scripts están hechos para realizar tareas pequeñas, de ejecución rápida y flexible para tareas o procesos automatizados.

Generalmente, estos lenguajes son interpretados y tienen tipado dinámico. Otra característica de estos lenguajes es que tienen una amplia variedad de librerías para simplificar la escritura del código, por lo que son muy fáciles de leer.

Los ejemplos más populares de este tipo de lenguajes son JavaScript y Python.

# 15. ¿Existen otros paradigmas? Justifique la respuesta

Existen otros paradigmas que no vimos en la práctica, como el declarativo, el declarativo o el dirigido por eventos. Pero la realidad es que en la actualidad es difícil encontrar un lenguaje que esté orientado exclusivamente a un paradigma; generalmente usan una combinación de las características de varios.

Por ejemplo, JavaScript es un lenguaje principalmente basado en Scripts, pero permite la implementación de objetos y tiene características de lenguajes funcionales.