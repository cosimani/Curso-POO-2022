.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 10 - POO 2022
===================
(Fecha: 28 de abril)


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

	QGroupBox * grupo = new QGroupBox( "Texto" );
	QGridLayout * layout = new QGridLayout;
	
	layout->addWidget( label, 0, 0 );
	layout->addWidget( usuario, 1, 0, 1, 2 );
	layout->addWidget( clave, 2, 0, 1, 2 );
	
	grupo->setLayout( layout );



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

- Punto de partida: Proyecto del Ejercicio Clase 09  
- Explicar a medida que va escribiendo código, la creación de un QWidget vacío para visualizarlo cuando el usuario ingresado sea válido. 
- También se puede explicar con voz en off.








