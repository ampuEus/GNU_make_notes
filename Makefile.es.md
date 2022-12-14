# Introducción a los Makefile-s
>NOTA: Aunque los ejemplos que se van a utilizar en esta guia son para el lenguaje C, `make` puede ser utilizado en otros lenguajes de programación que dispongan de compilador o simpliemente para link-ar diferentes archivos

## Índice
***TODO***

## ¿Para que se usa `make`?


## Introducción
Para poder usar el comando `make`, primero es necesario definir el archivo `makefile` que describa las relaciones entre los archivos del programa y proporcione comandos para actualizar cada archivo.

> En un programa, por lo general, el archivo ejecutable se actualiza a partir de archivos de objetos, que a su vez se crean mediante la compilación de archivos de origen. p. ej.: *.exe -> *.o -> *.c

Una vez hecho el `makefile`, cada vez que cambia algún archivo fuente, solo hay que ejecutar el comando de shell `make`.

El programa `make` utiliza la información del `makefile` junto con los tiempos de la última modificación de los archivos para decidir cuáles de estos archivos necesitan ser actualizados/recompilados.

Cuando `make` recompila:
  - Cada archivo fuente (\*.c) modificado vuelve a compilarse
  - Si un archivo de encabezado (\*.h) ha cambiado, cada archivo fuente C que incluya el *header* debe volver a compilarse para que sea seguro
  - **TODO - ¿PORQUÉ?->** Cada compilación produce un archivo objeto (*.o) correspondiente al archivo fuente
  - **TODO - NO ENTIENDO ESTO ->** Finalmente, si se ha vuelto a compilar cualquier archivo de origen, todos los archivos de objeto, ya sean nuevos o guardados de compilaciones anteriores, deben vincularse para producir el nuevo ejecutable

## Lexico de un Makefile
### Reglas
#### Reglas implicitas
#### Variables utilizadas por reglas implicitas
Estas son algunas de las variables más comunes utilizadas como nombres de programas en reglas implicitas:
| Variable | Descripcion                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| AR       | Programa de mantenimiento de archivos; por defecto 'ar'.                                                    |
| AS       | Programa para compilar archivos de ensamblador; por defecto 'como'.                                         |
| CC       | Programa para compilar programas en C; por defecto 'cc'.                                                    |
| CXX      | Programa para compilar programas C++; predeterminado 'g ++'.                                                |
| CPP      | Programa para ejecutar el preprocesador C, con resultados a la salida estándar; predeterminado '$ (CC) -E'. |
| RM       | Comando para eliminar un archivo; por defecto 'rm -f'.                                                      |

Además, la siguiente tabla de variables son argumentos adicionales para los programas anteriores:

*Los valores predeterminados para todos estos son la cadena vacía, a menos que se indique lo contrario.*
| Variable | Descripción                      |
|----------|----------------------------------|
| ARFLAGS  | Flag para el programa de mantenimiento de archivos; por defecto 'rv'.                             |
| ASFLAGS  | Indicadores adicionales para dar al ensamblador (cuando se invocan explícitamente en un archivo '.s' o '.S').                                                 |
| CFLAGS   | Indicadores adicionales para dar al compilador de C.                                              |
| CXXFLAGS | Indicadores adicionales para dar al compilador de C++.                                            |
| CPPFLAGS | Indicadores adicionales para dar al preprocesador de C y a los programas que lo usan (los compiladores de C y Fortran).                                       |
| LDFLAGS  | Indicadores adicionales para dar a los compiladores cuando se supone que deben invocar el enlazador, 'ld', como -L. En su lugar, se deben agregar bibliotecas (-lfoo) a la variable LDLIBS.                                    |
| LDLIBS   | Indicadores de biblioteca o nombres dados a los compiladores cuando se supone que deben invocar al enlazador, 'ld'. LOADLIBES es una alternativa en desuso (pero aún admitida) a LDLIBS. Los indicadores del enlazador que no son de biblioteca, como -L, deben ir en la variable LDFLAGS. |

### Variables
#### Automatic variables
#### Variable assignment
### Manipulación de texto

## Un Makefile simple
```makefile
edit : main.o kbd.o command.o display.o \
       insert.o search.o files.o utils.o
        cc -o edit main.o kbd.o command.o display.o \
                   insert.o search.o files.o utils.o

main.o : main.c defs.h
        cc -c main.c
kbd.o : kbd.c defs.h command.h
        cc -c kbd.c
command.o : command.c defs.h command.h
        cc -c command.c
display.o : display.c defs.h buffer.h
        cc -c display.c
insert.o : insert.c defs.h buffer.h
        cc -c insert.c
search.o : search.c defs.h buffer.h
        cc -c search.c
files.o : files.c defs.h buffer.h command.h
        cc -c files.c
utils.o : utils.c defs.h
        cc -c utils.c
clean :
        rm edit main.o kbd.o command.o display.o \
           insert.o search.o files.o utils.o
```



## Referencias
https://www.gnu.org/software/make/manual/make.html
