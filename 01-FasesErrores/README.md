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
   Resultado: Arroja un warning por la declaracion implicita de la funcion prontf.
   ```bash
       hello4.c: In function ‘main’:
	   hello4.c:10:2: warning: implicit declaration of function ‘prontf’; did you mean ‘printf’? [-Wimplicit-function-declaration]
  	   prontf("La respuesta es %d\n");
  	   ^~~~~~
  	   printf
                               ~^

8) En el hello4.s se ve el codigo assembler generado como resultado a lo ejecutado en el punto anterior.

9) #### Comando ejecutado: *gcc -std=c11 hello4.S -c -o hello4.o
   hello4.o* contiene el binario generado.

10) #### Comando ejecutado: gcc -std=c11 hello4.o -o hello4 -L /usr/include/stdlib.h
	Resultado: Error, el linker no pudo encontrar ninguna referencia a prontf en stdlib.
	```bash
	hello4.o: En la función main':
	hello4.c:(.text+0x1a): referencia a `prontf' sin definir
	collect2: error: ld returned 1 exit status

11) #### Comando ejecutado: gcc -std=c11 hello5.c -o hello5
	Resultado: Al generar un ejecutable tira un warning por la referencia que se hace al digito dentro de printf.
	```bash
	hello5.c: In function ‘main’:
	hello5.c:11:30: warning: format ‘%d’ expects a matching ‘int’ argument [-Wformat=]
    printf("La respuesta es %d\n");


12) Resultado: Cuando se ejecuta hello5 se esperaria que se muestre por pantalla "La respuesta es 42", pero al no pasarle por parametro a la funcion printf el digido %d, esta imprime valores extraños.

13) Resultado: Luego de corregir el error que se producía en el punto anterior, ahora la salida por patalla muestra el resultado que se esperaba: "La respuesta es 42"

15) #### Comando ejecutado: gcc -std=c11 -o hello7 hello7.c
	Resultado: Esto funciona porque el compilador siempre linkea con la libreria de C, donde esta definida printf.
	
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



