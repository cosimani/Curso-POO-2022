.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 11 - POO 2022
===================
(Fecha: 29 de abril)



Sutilezas con punteros
^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	char cadena[ 10 ] = "hola";  
	// Funciona? sí. Qué hace con el sobrante?
	// Los completa a todos con \000

	char cadena[ 4 ] = "hola";   // Por qué no compila?

	char cadena[ 5 ] = "hola";   // Y por qué esto sí compila?

	// Porque la última posición se usa para el carácter nulo que el
	// compilador lo agrega (si tiene lugar).

	//    \000  (octal)
	//    \x0   (hexadecimal)    

Usando puntero para cadenas
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	char * cadena = "hola";      // el compilador agrega \000
	char * cadena = "ho\000la";  // Imprime  ho

- Asignamos memoria dinámicamente.
- No necesitamos especificar la longitud máxima.

Notación octal y hexadecimal
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	cout << 3 + 4 + 11;      // Imprime 18
	cout << 3 + 4 + 011;     // ?

	//    octal    hexadecimal    decimal
	//    0121     0x51           81
	//    011      0x9            9
	//    '\000'   '\x0'          nulo
	//    '\063'   '\x33'         carácter 3

Punteros a punteros
^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	char cadena[ 2 ][ 3 ];
	cadena[ 0 ][ 0 ] = 'f';
	cadena[ 0 ][ 1 ] = 'u';
	cadena[ 0 ][ 2 ] = 'e';
	cadena[ 1 ][ 0 ] = 'f';
	cadena[ 1 ][ 1 ] = 'u';
	cadena[ 1 ][ 2 ] = 'i';

	//    Mejor así

	char cadena[ 2 ][ 3 ];
	cadena[ 0 ][ 0 ] = 's';
	cadena[ 0 ][ 1 ] = 'i';
	cadena[ 0 ][ 2 ] = '\000';
	cadena[ 1 ][ 0 ] = 'n';
	cadena[ 1 ][ 1 ] = 'o';
	cadena[ 1 ][ 2 ] = '\000';
 
Array ≡ puntero
^^^^^^^^^^^^^^^

- Cuando declaramos un array
- Estamos declarando un puntero al primer elemento.

.. code-block:: c

	char arreglo[ 5 ];
	char * puntero;
	puntero = arreglo;  // Equivale a puntero = &arreglo[ 0 ];

Volviendo a puntero a puntero
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	char cadena[ 2 ][ 3 ] = { { 's', 'i', '\000' }, { 'n', 'o', '\000' } };
	// Y si fuera char cadena[ 2 ][ 3 ] = { { 's', 'i', '-' }, { 'n', 'o', '\000' } };
	char * p1;
	char * p2;

	p1 = cadena[ 0 ];   // p1 = &cadena[ 0 ][ 0 ];
	p2 = cadena[ 1 ];   // p2 = &cadena[ 1 ][ 0 ];

	cout << p1;  // si  
	cout << p2;  // no
	
	cout << *p1;  // ?
	cout << *p2;  // ?

	// Es decir:
	//    El identificador de un arreglo unidimensional 
	//    es considerado un puntero a su primer elemento.

**Ejemplo**

.. code-block:: c

	char p1[] = { 'a', 'b', 'c', 'd', 'e' };
	cout << "Letra " << *p1;   // Letra a
	cout << "Letra " << p1[ 0 ];   // Letra a

	char m2[][ 5 ] = { { 'a', 'b', 'c', 'd', 'e' }, { 'A', 'B', 'C', 'D', 'E' } };
	cout << "Letra " << **m2;          // Letra a
	cout << "Letra " << m2[ 0 ][ 0 ];      // Letra a
	cout << "Letra " << m2[ 1 ][ 3 ];      // Letra D
	cout << "Letra " << *( *( m2 + 1 ) + 3 );  // Letra D

**Extendiendo a arreglos de cualquier dimensión**

.. code-block:: c

	m[ a ] == *( m + a )
	m[ a ][ b ] == *( *( m + a ) + b )
	m[ a ][ b ][ c ] == *( *( *( m + a ) + b ) + c )

	//    Si nos referimos al primer elemento

	m[ 0 ] == *m
	m[ 0 ][ 0 ] == **m
	m[ 0 ][ 0 ][ 0 ] == ***m


**Array como parámetro en funciones**

.. code-block:: c

	#include <iostream>
	using namespace std;

	void funcion( int miArray[] );
	// Le estamos pasando un puntero al primer elemento del array.

	int main()  {
	    int miA[ 5 ] = { 0, 1, 2, 3, 4 };

	    funcion( miA );

	    cout << miA[ 0 ] << miA[ 1 ] << miA[ 2 ] << miA[ 3 ] << miA[ 4 ];
	}

	void funcion( int miArray[] )  {
	    miArray[ 0 ] = 5;  // Las modificaciones quedarán.

	    miArray[ 3 ] = 5; 
	} 



Parámetros desde la línea de comandos
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Escribir el siguiente programa y ejecutarlo desde la línea de comandos incluyendo parámetros:

.. code-block:: c

	#include <iostream>

	int main( int argc, char ** argv )  {
	    std::cout << "Hay " << argc << " argumentos:" << std::endl;
	    for ( int i = 0 ; i < argc ; ++i ) {
	        std::cout << argv[ i ] << std::endl;
	    }
	}


	
**Ejercicio:** Comenzar un proyecto vacío con QtCreator y diseñar un login de usuarios:
 
.. figure:: imagenes/login.png 

- Tendrá un tamaño de 250x120 píxeles y llevará por título "Login".
- El único usuario válido es: (DNI del alumno):(últimos 3 números del DNI)
- Ocultar con asteriscos la clave.
- Si el usuario y clave no es válido, sólo el campo de la clave se deberá limpiar.
- Al fallar la clave 3 veces, la aplicación se cierra. 
- Si el usuario es válido, entonces se oculta el login y se visualiza un nuevo QWidget como el que sigue:

.. figure:: imagenes/ventana.png

- Utilizar una imagen del disco aproximadamente de 100x100 píxeles.
- Esta imagen se mostrará en el QWidget exactamente centrada.
- Dibujar además un cuadrado que envuelva la imagen (como muestra el ejemplo).
- La ventana puede tener cualquier tamaño pero llevará por título "Ventana".



QByteArray
^^^^^^^^^^

- Se podría decir que es administrador de un char*
- Se puede usar el operador []
- Almacena \\000 al final de cada objeto QByteArray



El preprocesador
^^^^^^^^^^^^^^^^

-	Analiza el archivo fuente antes de la compilación real
-	Realiza las sustituciones de macros
-	Una macro es un patrón de sustitución formado por expresiones textuales
-	Procesa las directivas (``#include``, ``#define``, ``#ifndef``, ...)
-	Elimina los comentarios.

**Directivas #ifdef #endif #ifndef**

- Con ``#ifdef`` si la macro está definida, entonces hace lo siguiente hasta encontrar un ``#endif``
- ``#ifndef`` pregunta si no está definida

**Directiva #include**

- Inserta archivos
- Influye sobre el ámbito y los identificadores

.. code-block:: c

	#include <nombre de fichero cabecera>
	#include "nombre de fichero de cabecera"

**Directiva #define**

- Define macros para sustituir cada vez que se encuentre el identificador.

.. code-block:: c

	#define identificador <secuencia>
	
-	Si 'secuencia' no existe, el identificador será eliminado cada vez que aparezca
-	No es necesario añadir un punto y coma al final
-	Termina en el primer retorno de línea encontrado
-	Podríamos definir un nuevo lenguaje
 
.. figure:: imagenes/define.png


**Ejercicio:**

- Nuevo proyecto Empty 
- Crear un .h vacío y definir una clase Persona con int edad y string nombre.
- En el archivo ``main.cpp`` incluir dos veces el archivo .h
- Tratar de resolver el problema sólo modificando el .h


Guardián de inclusión múltiple
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Este problema se soluciona con el uso del **Guardián de inclusión múltiple**:

.. code-block:: c

	#ifndef PRINCIPAL_H
	#define PRINCIPAL_H

	// . . . 

	#endif // PRINCIPAL_H



QTextEdit
^^^^^^^^^

- Un QWidget que muestra texto plano o enriquecido
- Puede mostrar imágenes, listas y tablas
- La barra de desplazamiento es automática
- Interpreta tags HTML
- Seteamos texto con setPlainText()



Ejercicio Clase 11
==================

- Crear una aplicación que inicie con un login validando el usuario admin:123
- Luego de ingresar el usuario válido, mostrar un nuevo QWidget con las siguientes características:
	- Definida en la clase Editor
	- Contendrá un QTextEdit vacío, un QPushButton "Buscar" y un QLabel
	- El usuario podrá escribir cualquier texto en el QTextEdit
	- Al presionar "Buscar" se detectará automáticamente la cantidad de letras 'a' en el texto y colocará el resultado en el QLabel.
- Luego de dejar funcionando lo anterior, agregar lo siguiente:
	- Un QLineEdit y un QPushButton "Borrar"
	- En este QLineEdit el usuario puede colocar una palabra o frase
	- Al presionar Borrar se buscará en el texto y se eliminarán


Entregable Clase 11
===================

- Punto de partida: Proyecto del Ejercicio Clase 10  
- Reemplazar el QWidget vacío por un QTextEdit.
- Explicar a medida que va escribiendo código o con voz en off.


