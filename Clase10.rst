.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 10 - POO 2022
===================
(Fecha: 28 de abril)


.. figure:: imagenes/java_vs_cplusplus.gif

- Para crear gifs a partir de videos en youtube en: https://gifs.com 



QLineEdit
^^^^^^^^^

.. code-block:: c

	QLineEdit * le = new QLineEdit;
	le->setEchoMode( QLineEdit::Password );
	le->setEnabled( false );

	// QLineEdit::Normal  // Se visualizan al escribir
	// QLineEdit::NoEcho  // No se visualiza nada
	// QLineEdit::Password  // Se escribe como asteriscos
	// QLineEdit::PasswordEchoOnEdit  // Se escribe normal y al dejar de editar se convierten en asteriscos

**Señales**

.. code-block:: c

	// void returnPressed()  // Detecta cuando el usuario presiona Enter.

	// void editingFinished()  // Cuando pierde foco.

	// void textChanged( const QString & text )  // Texto modificado por código o por usuario desde la gui.

	// void textEdited( const QString & text )  // Sólo por el usuario.



QGroupBox
^^^^^^^^^ 

.. figure:: imagenes/qgroupbox.png

.. code-block:: c

	QGroupBox* grupo = new QGroupBox("Texto");
	QGridLayout* layout = new QGridLayout;
	
	layout->addWidget(label, 0, 0);
	layout->addWidget(usuario, 1, 0, 1, 2);
	layout->addWidget(clave, 2, 0, 1, 2);
	
	grupo->setLayout(layout);



**Constructores con argumentos por defecto**

.. code-block:: c

	class ClaseA  {
	public:
	    ClaseA( int a = 10, int b = 20 ) : a( a ), b( b )  {  }
	
	    void verDatos( int &a, int &b )  {
	        a = this->a;
	        b = this->b;
	    }

	private:
	    int a, b;
	};

	int main( int argc, char ** argv )  {
	    ClaseA * objA = new ClaseA;

	    int a, b;
	    objA->verDatos( a, b );
	
	    std::cout << "a = " << a << " b = " << b << std::endl;

	    return 0;
	}

	// Probar con:	
	
	ClaseA( int c, int a = 10, int b = 20 ) : a( a ), b( b ), c( 0 )  {  }

	ClaseA( int a = 10, int b = 20, int c ) : a( a ), b( b ), c( 0 )  {  }



**Ejercicio:** Escribir la salida por consola de la siguiente aplicación:

.. code-block:: c

	#include <QApplication>
	#include <QDebug>

	int main( int argc, char** argv )  {
	    QApplication app( argc, argv );

	    int a = 10, b = 100, c = 30, d = 1, e = 54;
	    int m[ 10 ] = { 10, 9, 80, 7, 60, 5, 40, 3, 20, 1 };
	    int *p = &m[ 3 ], *q = &m[ 6 ];

	    ++q;
	    qDebug() << a + m[ d / c ] + b-- / *q + 10 + e--;

	    p = m;
	    qDebug() << e + *p + m[ 9 ]++;

	    return 0;
	}


**Ejercicio**

- Crear un vector de 100 números enteros.
- Los valores serán aleatorios y positivos menores o iguales a 10.
- Utilizar un algoritmo para ordenar de menor a mayor estos números.


**Ejercicio**

- Crear dos ``std::vector``. Un ``vector< double >`` y un ``vector< double * >``.
- Agregar 10 elementos en cada uno.
- Averiguar cuál objeto ocupa más memoria. 
- Publicar por consola el tamaño.


**¿Cómo entregar ejercicios?**

- Luego de finalizar el desarrollo del programa, cerrar el proyecto de QtCreator.
- Eliminar el archivo .pro.user
- Comprimir la carpeta donde está el código fuente, no así la carpeta build- .





.. ..
 
 <!---  
 **Función con número indefinido de parámetros** 

 (para ocultar requiere una primer linea con .. ..    Los que queremos ocultar debe tener el menos un espacio)

 - Requiere:

 .. code-block:: c

 	#include <cstdarg>

 - Imprime los enteros que se pasen como parámetro
 - Se puede comprender la sintaxis de:

 .. code-block:: c

 	int printf(const char* format, ...)

 .. code-block:: c

 	void imprimirParametros(int cantidad, ...)  {

 	    // En cstdarg se define un tipo va_list y define tres macros (va_start, va_arg y va_end)
 	    // para moverse por la lista de argumentos cuyo numero y tipo no son conocidos.
 
 	    // Aqui se declara la lista de parametros
 	    va_list argumentos; 
 				
 	    // La macro va_start inicializa 'argumentos' para ser usado por va_arg y va_end.
 	    // 'cantidad' es el nombre del ultimo parametro antes de la lista de argumentos.
 	    va_start(argumentos, cantidad); 
 
 	    for (int i=0 ; i<cantidad ; i++)  {
 
 		    // La macro va_arg contiene el tipo y el valor del proximo argumento. 
 			// Cada llamada a va_arg devuelve el resto de los argumentos.
 
 	        int valor = va_arg( argumentos, int );  // Devuelve en formato de int
 
 	        cout << valor << endl;
 	    }
 
 	    // A cada invocacion de va_start le corresponde una invocacion de va_end
 	    // en la misma funcion. 	   
 	    va_end(argumentos);  // Para limpiar la pila de parametros
 	}
 	
 **Ejercicio:** 
 
 - Definir una función (que se llame mi_printf) que realice el mismo trabajo que la famosa printf. 
 - Investigar qué tipos de datos se pueden utilizar en va_arg
 
 
 **Se puede pasar cualquier tipo siempre que sea con punteros:**
  
 .. code-block:: c
  
 	#include <QApplication>
 	#include <QString>
 	#include <QDebug>
 	#include <cstdarg>
 
 	void imprimirParametros(int cantidad, ...)  {
 	    va_list argumentos; // esta linea declara la lista de parametros
 	    va_start(argumentos, cantidad);
 
 	    for (int i=0 ; i<cantidad ; i++)  {
 	        QString *str = va_arg( argumentos, QString* );
 	        qDebug() << *str;
 	    } 
 
 	    va_end(argumentos);  // Para limpiar la pila de parametros
 	}
 
 	int main(int argc, char** argv)  {
 	    QApplication app(argc, argv);
 
 	    imprimirParametros(3, new QString("uno"), new QString("dos"), new QString("tres"),
 	                       new QString("cuatro"), new QString("cinco"));
 
 	    return 0;
 	}
 --->
 

**Ejercicio**

- Utilizar el login del ejercicio anterior en un proyecto nuevo.
- Definir la clase Formulario que será un QWidget
- Formulario tendrá QLabels y QLineEdits para Legajo, Nombre y Apellido y un QPushButton
- Si la clave ingresada es admin:1111, se cierra Login y se muestra Formulario

Ejercicio Clase 10
==================

.. figure:: imagenes/ejercicio_captcha.jpg
	

Entregable Clase 10
===================

- Punto de partida: Proyecto vacío
- Explicar a medida que va escribiendo código, la creación de un QGridLayout para un login 
- También se puede explicar con voz en off











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
	puntero = arreglo;  // Equivale a puntero = &arreglo[0];

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

	int main( int argc, char** argv )  {
	    std::cout << "Hay " << argc << " argumentos:" << std::endl;
	    for ( int i = 0; i < argc; ++i ) {
	        std::cout << argv[ i ] << std::endl;
	    }
	}








	
**Ejercicio 15:** Comenzar un proyecto vacío con QtCreator y diseñar un login de usuarios:
 
.. figure:: images/clase07/login.png 

- Tendrá un tamaño de 250x120 píxeles y llevará por título "Login".
- El único usuario válido es: (DNI del alumno):(últimos 3 números del DNI)
- Ocultar con asteriscos la clave.
- Si el usuario y clave no es válido, sólo el campo de la clave se deberá limpiar.
- Al fallar la clave 3 veces, la aplicación se cierra. 
- Si el usuario es válido, entonces se oculta el login y se visualiza un nuevo QWidget como el que sigue:

.. figure:: images/clase07/ventana.png

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
 
.. figure:: images/clase07/define.png


**Ejercicio 16:**

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

**Ejercicio 17**

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


