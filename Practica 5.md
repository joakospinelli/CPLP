# 1. Explique claramente cual es la utilidad del registro de activación y que representan cada una de sus partes.

| Parte | Descripción |
| ----- | ----------- |
| Head | ? XD |
| Punto de Retorno | Contiene la dirección hacia la que se debe continuar la ejecución una vez que este bloque termina. |
| Enlace estático | Contiene un puntero hacia la dirección del registro donde se **declaró** este bloque |
| Enlace dinámico | Contiene un puntero hacia la dirección del registro donde se **llamó** a este bloque |
| Variables | Almacena las variables del bloque y los valores que toma durante su ejecución |
| Parámetros | Almacena los parámetros que se reciben al llamar al bloque |
| Procedimientos | Almacena los procedimientos declarados dentro del bloque |
| Funciones | Almacena las funciones declaradas dentro del bloque |
| Valor de retorno | Almacena los valores de las rutinas llamadas |

# 2. Dado el siguiente programa escrito en Pascal-like, continuar la realización de las pilas de ejecución hasta finalizar las mismas
```pascal
Program Main
    Var a: array[1..10] of integer;
    x,y,z:integer

    Procedure A ()
    var y,t: integer;
    begin
        a(1):= a(1)+1;z:=z+1;
        t:=1; y:=2;
        B(); a(y):=a(y)+3; y:=y+1;
        If z=11 Then Begin
            a(z-1):=a(z-2) + 3;
            z:=z-4;
            a(z-y):=a(z) – a(y) + 5;
        End;
    end;

    Function t():integer
    begin
        y:=y+1; z:=z-6;
        return(y+x);
    end;

    Procedure B()
    var d:integer;
        Procedure I ()
            begin
            x:=0; x:=x+6;
            end;
        begin
        x:=x+t; d:=0;
        while x>d do begin
            I(); x:=x-1;
            d:=d + 2;
        end;
    end;

begin
    For x:=1 To 10 do a(x):=x;
    x:=5; y:=1; z:=10;
    A();
    For x:=1 To 10 do write(a(x),x);
end.
```

## a. Cadena estática:

<img src="./img/Practica 5/ej2estatica.png">

## b. Cadena dinámica:

<img src="./img/Practica 5/ej2dinamica.png">