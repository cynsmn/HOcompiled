Compilador
-------------------------------------------------
1. Ejecutamos make proprocessing:
     gcc -E calculator.c -o calculator.pp 
2. Se genera un archivo que es calculator.pp
3. Ejecutando make assembler:
     gcc -masm=intel -S calculator.c -o calculator.asm 
     se generaron los archivos calculator.asm
   Las funciones (son las que llama por call) que usa el calculator.asm son
     add_numbers
     printf
4. Para crear el objeto ejecuto make object:
     gcc -c calculator.c -o calculator.o
   Se genero el archivo .o
   Para ver los descriptores del objeto hago:
$ nm calculator.o 
000000000000003c T add_numbers  ==> texto
0000000000000000 T main         ==> texto
                 U printf       ==> esta funcion es undefined
   Tengo 3 funciones: main, add_numbers y printf no
   
   Genero el ejecutable:
     gcc calculator.o -o calculator.e
     Ahora veo los descriptores del ejecutable:
$ nm calculator.e 
aparece una lista larga con todos los descriptores, pero printf sigue 
undefined: 
0000000000400572 T add_numbers
....
....
.... 
0000000000400536 T main
                 U printf@@GLIBC_2.2.5
Pero ahora, el ejecutable le dice que linkee cuando ejecuta (con el @@) con 
una libreria dinamica que se llama GLIB_2.2.5 al ejecutarse. 
En todo elproceso de la compilacion esta undefined.
Las librerias estaticas (definidas por ejemplo con U) las pega completas 
dentro del codigo, en vez de que se llamen desde otro lugar.

5. El simbolo en el ejecutable agrego un link a una libreria a la que llama 
cuando se ejecuta. Mientras que en toda la compilacion la funcion printf 
queda undefined.




 

