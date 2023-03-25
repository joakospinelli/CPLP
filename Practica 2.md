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
T = {  'A'...'Z', 'a'...'z', '0'...'9', ' ' }
S = { <palabra> }
P = { 
    <palabras> ::= <caracter><palabra> | <caracter>
    <caracter> ::= 'A'...'Z' | 'a'...'z' | '0'...'9' | ' '
}
```

# 7. Defina en EBNF la gramática para la definición de números reales. Inténtelo desarrollar para BNF y explique las diferencias con la utilización de la gramática EBNF.

EBNF:
```bnf
G = (N, S, T, P)

N = { <real>, <digito> }
T = { 0..9, '.' }
S = { <real> }
P = {
    <real> ::= [('+'|'-')] {<digito>}+ ['.' {<digito>}+]
    <digito> ::= 0..9
}
```

# 8. Utilizando la gramática que desarrolló en los puntos 6 y 7, escriba el árbol sintáctico de:

### a. Conceptos

<img src="./img/Practica 2/p2ej8a.png">

### b. Programación

<img src="./img/Practica 2/p2ej8b.png">

### c. 1255869

zzz

### d. 854,26

<img src="./img/Practica 2/p2ej8d.png">

### e. Conceptos de lenguajes

zzz

#  9. Defina utilizando diagramas sintácticos la gramática para la definición de un identificador de un lenguaje de programación. Tenga presente como regla que un identificador no puede comenzar con números.

<img src="./img/Practica 2/p2ej9.png">

# 10.
### a. Defina con EBNF la gramática para una expresión numérica, dónde intervienen variables y números. Considerar los operadores +, -, * y / sin orden de prioridad. No considerar el uso de paréntesis.

```bnf
G = (N, S, T, P)

N = { <expresion>, <numero>, <operador>, <digito> }
T = { '0'..'9', '+', '-', '*', '/', 'a'...'z' }
S = { <expresion> }
P = { 
    <expresion> ::= (<numero> | <variable>) {<operacion>}+
    <operacion> ::= <operador> (<numero> | <variable>)
    <variable> ::= {<caracter>}+
    <numero> ::= {<digito>}+
    <caracter> ::= ( 'a' | ... 'z' )
    <digito> ::= ( '0' | ... | '9' )
    <operador> ::= ( '+' | '-' | '*' | '/' )
}
```

### b. A la gramática definida en el ejercicio anterior agregarle prioridad de operadores.

```bnf
Siguiendo la gramática del ejercicio anterior

P = { 
    <expresion> ::= (<numero> | <variable>) {<suma_resta>}+
    <operacion> ::= ( <mul_div>(<numero> | <variable>) | (<numero> | <variable>) )
    <mul_div> ::= ( '*' | '/' ) <operacion>
    <suma_resta> ::= ( '+' | '-' ) <operacion>
    <variable> ::= {<caracter>}+
    <numero> ::= {<digito>}+
    <caracter> ::= ( 'a' | ... 'z' )
    <digito> ::= ( '0' | ... | '9' )
}
```

### c. Describa con sus palabras los pasos y decisiones que tomó para agregarle prioridad de operadores al ejercicio anterior.

Para definir las prioridades hay que tener en cuenta la separación en términos de las expresiones matemáticas; las sumas y las restas son los identificadores para separar términos, por lo que las multiplicaciones y divisiones tienen mayor prioridad.

Sabiendo esto, definimos en la expresión una repetición de operaciones de suma-resta, y dentro de estas definimos las multiplicaciones y divisiones.

# 11. La siguiente gramática intenta describir sintácticamente la sentencia for de ADA, indique cuál/cuáles son los errores justificando la respuesta.
```bnf
N= {<sentencia_for>, <bloque>, <variable>, <letra>, <cadena>, <digito>, <otro>, <operacion>, <llamada_a_funcion>, <numero>, <sentencia> }

P= {
    <sentencia_for>::= for (i= IN 1..10) loop <bloque> end loop;
    <variable>::= <letra> | <cadena>
    <cadena>::= { ( <letra> | <digito> | <otro> ) }+
    <letra>::=( a | .. | z | A | .. | Z )
    <digito>::= ( 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 0 )
    <bloque>::= <sentencia> | <sentencia> <bloque> | <bloque> <sentencia>
    <sentencia>::= <sentencia_asignacion> | <llamada_a_funcion> | <sentencia_if> | <sentencia_for> | <sentencia_while> | <sentencia_switch>
}
```

* `<otro> - <operación> - <llamada_a_funcion> - <numero>` no están definidos en *P*.
* Está mezclando las técnicas de recursión de BNF con EBNF.
* La definición de `<bloque>` es ambigua, porque el mismo resultado se puede obtener tanto desde `<sentencia> <bloque>` como  `<bloque> <sentencia>`.
* `<sentencia_asignacion> - <sentencia_if> - <sentencia_while> - <sentencia_switch>` no están declarados en *N* ni definidos en las producciones, pero aún así se usan para definir a otros no terminales.
* `<llamada_a_funcion>` no está definido en *P*.

# 12. Realice en EBNF la gramática para la definición un tag `div` en HTML5.

```bnf
G = (N, S, T, P)

N = { <div>, <abrirDiv>, <cerrarDiv>, <html>, <tag> }
T = { 'a'...'z', '<', '>', '/' }
S = { <expresion> }
P = { 
    <div> ::= <abrirDiv> { (<html> | <palabra>) }* <cerrarDiv>
    <html> ::= <tag> (<html> | <palabra>) <tagCierre>
    <tag> ::= '<' <palabra> {<attr>}* '>'
    <tagCierre> ::= '</' <palabra> '>'
    <attr> ::= <palabra> '=' '"' <palabra> '"'
    <abrirDiv> ::= '<div>'
    <cerrarDiv> ::= '</div>'
    <palabra> ::= {'a'..'z'}*
}
```

# 13. Defina en EBNF una gramática para la construcción de números primos. ¿Qué debería agregar a la gramática para completar el ejercicio?

No se puede hacer porque EBNF no se encarga de las operaciones aritmético-lógicas que defina el programador.

# 14. Sobre un lenguaje de su preferencia escriba en EBNF la gramática para la definición de funciones o métodos o procedimientos (considere los parámetros en caso de ser necesario)

Siguiendo la definición de funciones en JavaScript `function nombre(a,b){ ... }`

```bnf
G = (N, S, T, P)

N = { <funcion>, <parametros>, <palabra> }
T = { 'a'..'z' }
S = { <funcion> }
P = {
    <funcion> ::= 'function' <palabra> '(' [<parametros>] ')' '{' {<palabra>}* '}'
    <parametros> ::= { (<palabra> | ', '<palabra>) }*
    <palabra> ::= {letra}+
    <letra> ::= ('a' | ... | 'z') 
}
```