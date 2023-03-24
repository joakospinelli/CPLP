# 1. Complete el siguiente cuadro:

<img src="./img/Practica 2/p2ej1.png">

# 2. ¿Cuál es la importancia de la sintaxis para un lenguaje? ¿Cuáles son sus elementos?

La sintaxis es el conjunto de reglas definidas sobre cómo se conforman los caracteres para componer el programa.

Establece cómo deben combinarse los componentes básicos para formar sentencias y programas.

Los componentes de la sintaxis son:
* `Conjunto de caracteres:` representa el código de caracteres usado por el lenguaje, y los caracteres que éste brinda que pueden ser utilizados por el lenguaje para definir la sintaxis.
* `Operadores:` caracteres usados para representar operaciones aritmético-lógicas.
* `Palabras clave:` palabras que tienen sentido en un contexto específico.
* `Identificadores:` palabras clave asignadas por el programador durante la ejecución del programa. Nombres de variables, funciones, etc.
* `Palabras reservadas:` palabras clave que, además, no pueden ser usadas por el programador como identificadores.
* `Comentarios:` conjunto de caracteres usados para definir cómo hace el programador para escribir comentarios. Por ejemplo: // y /**/ en JavaScript, # en Python.

# 3. ¿Explique a qué se denomina regla lexicográfica y regla sintáctica?

Las reglas léxicas son aquellas que definen las palabras de un lenguaje a partir de los caracteres alfabético.

Las reglas sintácticas son aquellas que definen cómo se forman las expresiones y las sentencias del lenguaje.

# 4. ¿En la definición de un lenguaje, a qué se llama palabra reservadas? ¿A qué son equivalentes en la definición de una gramática? De un ejemplo de palabra reservada en el lenguaje que más conoce. (Ada, C, Ruby, Python, ...)

# 5. Dada la siguiente gramática escrita en BNF:
```java
G = (N, T, S, P)

N = {<numero_entero>, <digito> }
T = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9}
S = <numero_entero>
P = {
    <numero_entero>::=<digito><numero_entero> | <numero_entero><digito> | <digito>

    <digito> ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
}
```
### a. Identifique las componentes de la misma

Ya están definidos en el enunciado ??? no entendí

### b. Indique porqué es ambigua y corríjala

Es ambigua porque en la producción para definir `numero_entero` aparecen como posibilidades en la recursión los pares `<digito><numero_entero>` y `<numero_entero><digito>`. Esto implica que, al realizar el árbol de derivación va a haber más de una manera de definir algún valor de `numero_entero`, lo cual produce ambigüedad.

Para resolver esta ambigüedad hay que eliminar una de las dos posibilidades, por lo que quedaría de la siguiente manera:
```bnf
G = (N, T, S, P)

N = { <numero_entero>, <digito> }
T = { '0', '1', '2', '3', '4', '5', '6', '7', '8', '9' }
S = <numero_entero>
P = {
    <numero_entero> ::= <digito><numero_entero> | <digito>

    <digito> ::= '0' | '1' | '2' | '3' | '4' | '5' | '6' | '7' | '8' | '9'
}
```

# 6. Defina en BNF (Gramática de contexto libre desarrollada por Backus- Naur) la gramática para la definición de una palabra cualquiera.
```bnf
G = (N, S, T, P)

N = { <palabra>, <caracter> }
T = {  'A'...'Z', 'a'...'z', '0'...'9' }
S = { <palabra> }
P = { 
    <palabras> ::= <palabra><caracter> | <caracter>
    <caracter> ::= 'A'...'Z' | 'a'...'z' | '0'...'9'
}
```