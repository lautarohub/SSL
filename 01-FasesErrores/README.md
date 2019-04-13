2) #### Comando ejecutado: gcc -Wall -std=c11 -E hello2.c -o hello2.i 
   
   Resultado: No hubo errores al correr el comando.
   
   Análisis de contenido: Se generó un nuevo archivo preprocesado (.i) sin macros ni comentarios.
   
   *Nota: Las macros son aquellas notaciones de la pinta: #include <stdio.h> (o similares) que
   pueden hacer referencias a funciones u objetos que no esten declaradas dentro del .c preprocesado.*

3) Se crea hello3.c

4) Se declara una variable de tipo entera llamada printf, que recibe como primer parametro
   un arreglo constante de chars, y los tres puntos que vemos después se llaman *elipsis*
   e indican que la funcion puede recibir un numero arbitrario de parametros.

5) Asumo que se pedian diferencias entre hello2.i y hello3.i
   
   #### Comando ejecutado: gcc -Wall -std=c11 -E hello3.c -o hello3.i
   Resultado: No hubo errores al correr el comando.
   Las diferencias entre hello2.i y hello3.i es que el preprocesamiento del
   hello2.c tiene que preprocesar tambíen la llamada a la libreria estandar;
   mientras que en hello3 solo se preprocesa la declaracion de la función printf.
   La diferencia entre los preprocesamientos de ambos archivos es notable y se puede
   ver en la cantidad de lineas generadas en ambos archivos.
  

6) #### Comando ejecutado: gcc -Wall -std=c11 hello3.i -S -o hello3.S
   ```bash
   hello3.c: In function ‘main’:
   hello3.c:10:2: warning: implicit declaration of function ‘prontf’; did you mean ‘printf’? [-Wimplicit-function-declaration]
   prontf("La respuesta es %d\n");
   ^~~~~~
   printf
   hello3.c:10:2: error: expected declaration or statement at end of input
   hello3.c:9:5: warning: unused variable ‘i’ [-Wunused-variable]
   int i=42

7) #### Comando ejecutado: gcc -std=c11 hello4.c -S -o hello4.S
   ```bash
       hello4.c: In function ‘main’:
	   hello4.c:10:2: warning: implicit declaration of function ‘prontf’; did you mean ‘printf’? [-Wimplicit-function-declaration]
  	   prontf("La respuesta es %d\n");
  	   ^~~~~~
  	   printf
   Resultado luego de cambiar pront por print:
       hello4.c: In function ‘main’:
	   hello4.c:10:27: warning: format ‘%d’ expects a matching ‘int’ argument [-Wformat=]
       printf("La respuesta es %d\n");
                               ~^

8) En el hello4.s se ve el codigo assembler generado como resultado a lo ejecutado en el punto anterior.

9) Comando ejecutado: *gcc -std=c11 hello4.S -c -o hello4.o
   hello4.o* contiene el binario generado.

10) Comando ejecutado: *gcc -std=c11 -o hello4 hello4.c  -L /usr/include/stdlib.h*
	Resultado: No hubo errores.

11, 12, 13) No hubo errores, asi que salteo estos puntos.

15) #### Comando ejecutado: gcc -std=c11 -o hello7 hello7.c
	
  ```bash
	hello7.c: In function ‘main’:
	hello7.c:9:2: warning: implicit declaration of function ‘printf’ [-Wimplicit-function-declaration]
	  printf("La respuesta es %d\n", i);
	  ^~~~~~
	hello7.c:9:2: warning: incompatible implicit declaration of built-in function ‘printf’
	hello7.c:9:2: note: include ‘<stdio.h>’ or provide a declaration of ‘printf’
	hello7.c:1:1:
	+#include <stdio.h>
	 /* TP #1
	hello7.c:9:2:
	  printf("La respuesta es %d\n", i);
	  ^~~~~~



