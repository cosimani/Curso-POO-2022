.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 21 - POO 2022
===================
(Fecha: 3 de junio)



Registro en video de algunos temas de la clase de hoy
=====================================================

`QFile 2021 - https://youtu.be/Zf-yAkNmqso <https://youtu.be/Zf-yAkNmqso>`_ 



Clase QFile
^^^^^^^^^^^

- Permite leer y escribir en archivos. 
- Puede ser utilizado además con ``QTextStream`` o ``QDataStream``.

.. code-block:: c	

	QFile( const QString & name )
	viod setFile( const QString & name )

- Existe un archivo? y lo eliminamos.

.. code-block:: c	

	bool exists() const
	bool remove()

- Lectura de un archivo línea por línea:

.. code-block:: c	

	QFile file( "c:/in.txt" );
	if ( !file.open ( QIODevice::ReadOnly | QIODevice::Text ) )
	    return;

	while ( !file.atEnd() )  {
	    QByteArray linea = file.readLine();
	    qDebug() << linea;
	}



Práctica para parcial
=====================


**Ejercicio 1**

- Diseñar una aplicación que muestre en un ``QWidget`` cualquier imagen de 50x50
- La imagen deberá seguir al puntero del mouse cuando esté presionado un botón.
- Utilizar ``QTimer`` para actualizar la posición de la imagen dando un efecto inercial



**Ejercicio 2** 

- Crear un login con un QLabel que funcione como un QPushButton
- Para esto incorporar al QLabel la señal ``void signal_click()``


**Ejercicio 3** 

- Incorporar a un Login una señal que se emita cada vez que un usuario se valide exitosamente
- Que la señal se llame ``void signal_usuarioLogueado( QString )``
- El QString que envía es el nombre de usuario


**Ejercicio 4**

- Diseñar una aplicación con un login inicial que valide contra la base
- Almacenar el hash MD5 de las contraseñas
- Si el usuario es válido mostrar cualquier otra ventana 
- Registrar en la tabla 'logs' los intentos fallidos de logueo. No registrar las claves.


**Ejercicio 5**

- Definir la clase TuLabel que herede de QLabel
- Agregar un QLabel a la GUI y promoverlo a TuLabel
- Agregar un método ``void cambiarTexto( QString nuevoTexto )``
- Usar ese método desde la clase Principal de la siguiente forma:

.. code-block::

	ui->tuLabel->cambiarTexto( "Sos un TuLabel?" );


**Ejercicio 6**

- Elegir un archivo de texto cualquiera con ``QFileDialog`` y mostrarlo sobre un ``QTextEdit``.
- Agregar dos ``QLineEdit``, uno acompañado con el ``QLabel`` "Buscar" y otro con el "Reemplazar por".
- Un botón "Reemplazar" realizará la busqueda y reemplazará todas las coincidencias encontradas.


**Ejercicio 7** 

- Definir dos QWidgets (una clase Login y una clase Ventana).
- El Login validará al usuario contra una base SQLite
- Ventana sólo mostrará un QPushButton para "Volver" al login.
- Crear solamente un objeto de Ventana y uno solo de Login.


**Ejercicio 8**

- Comenzar un proyecto vacío con QtCreator y diseñar el siguiente login de usuarios:
 
.. figure:: imagenes/login.png  

- Este login tendrá las siguientes características:
	- Cuidar muy bien el layout. Notar la ubicación del botón con respecto a los campos.
	- Definido en la clase Login en los archivos login.h y login.cpp.
	- La ventana tendrá un tamaño de 250x120 píxeles y llevará por título "Login".
	- El único usuario válido es (DNI del alumno):(últimos 4 números del DNI)
	- Ocultar con asteriscos la clave.
	- Si el usuario y clave no es válido, sólo el campo de la clave se deberá limpiar.
	- Al fallar la clave 3 veces, la aplicación se cierra. 

- Si el usuario es válido, entonces se ocultará el login y se visualizará un nuevo QWidget como el que sigue:

.. figure:: imagenes/ventana.png  
 
- Este widget tendrá las siguientes características:
 	- Definido en la clase Ventana en los archivos ventana.h y ventana.cpp.
	- Con QNetworkAccessManager descargar una imagen cualquiera de 100x100 píxeles.
	- Esta imagen se mostrará en el QWidget centrada (como muestra el ejemplo).
	- Dibujar además un cuadrado que envuelva la imagen (como muestra el ejemplo).
	- La ventana puede tener cualquier tamaño y llevará por título "Ventana".


**Ejercicio 9** 

- Definir la siguiente jerarquía de clases:
 
.. figure:: imagenes/clases.png 

- Se pedirá definición de atributos y métodos (en papel y sin utilizar material de consulta)
- Instanciar objetos de estas clases.
- Prestar atención sobre los punteros a objetos, ámbitos, parámetros en funciones, modificadores de acceso, ...

**Ejercicio 10** 

- Aritmética de punteros en papel
- Escribir la salida por consola 

.. code-block:: c

	#include <QApplication>
	#include <QDebug>

	int main(int argc, char** argv)  {
	    QApplication app(argc, argv);

	    int a = 10, b = 10, c = 10, d = 10, e = 10;
	    int m[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
	    int *p = &m[2], *q = &m[4];

	    qDebug() << a + m[d/c] + b-- / *q + 10 + e--;
	    p = m;
	    qDebug() << e + *p + m[4]++;

	    return 0;
	}
	

**Ejercicio 11**

- Crear un std::vector para contener int
- Cargar 50 valores pseudo aleatorios entre 10 y 50
- Publicar el promedio y una lista con todos los números ordenados de mayor a menor


**Ejercicio 12**

- Crear una función genérica que imprima en un QTextEdit los valores ordenados de un array que se le pasa por parámetro
- Es decir, se le pasa un array con sus valores desordenados (o no), y la función genérica los devuelve ordenados
- Que el prototipo sea: ``template < class T > void imprimir( T * v, int cantidad, bool mayor_a_menor );``
- Utilizar el método de ordenamiento burbuja


**Ejercicio 13**

- Crear una clase Jugador con atributos ``int velocidad``, ``int fuerza`` y ``std::string nombre``
- Usar constructor inicializando de la manera recomendada la velocidad en 0, fuerza en 0 y nombre "sin nombre" 
- Crear los métodos setter y getter para setear y obtener los valores de los atributos
- Incluir el destructor
- Utilizar un ``std::vector< Jugador >`` e insertar 10 jugadores distintos
- Publicar en un QTextEdit todos los Jugadores

**Ejercicio 14**

- Descargar una imagen desde internet
- Mostrarla en un QWidget en un tamaño 100x100 píxeles
- Colocar un QSlider que permita modificar su tamaño, ampliando y reduciendo


**Ejercicio 15**

- Crear un Login de usuario utilizando QGridLayout, sin utilizar QtDesigner


**Ejercicio 16**

- Definir un formulario (en la clase Formulario)
- Formulario tendrá QLabels y QLineEdits para Legajo, Nombre y Apellido y un QPushButton
- Insertar un Captcha utilizando un QGroupBox
- Utilizar números aleatorios para el captcha de 4 dígitos

**Ejercicio 17**

- Crear una jerarquía de clases en donde la clase Persona sea la clase base.
- Cliente y Usuario derivan de Persona.
- Coloque las características más comunes que deberían tener estas clases.
- Utilizar las formas de definir estas clases como lo visto en la asignatura
- Utilizar const de la manera recomendable

**Ejercicio 18**

- Descargar una imagen de internet
- Mostrar en el centro de un QWidget y que rote sobre su centro


**Ejercicio 19**

- Crear una clase Barra que tenga funcionalidad de una barra de progreso (que no herede de QProgressBar)
- Debe tener métodos para setear su valor en porcentaje
- Usar la señal de ``downloadProgress`` de ``QNetworkReply``
- Crear una interfaz que tenga un ``QLineEdit`` para la URL y una Barra.
- Probarlo con alguna URL que pertenezca a un archivo con un tamaño para que la Barra se note su progreso

**Ejercicio 20**

- Diseñar una galería de fotos.
- Debe tener una base con una tabla 'imagenes' que tenga las URLs de imágenes
- Un botón >> y otro << para avanzar o retroceder en la galería de fotos
- Se podrá navegar sobre las fotos que se descargarán desde internet


**Ejercicio 21**

- En un QWidget dibujar una imagen de un fútbol con formato PNG (para usar transparencias)
- Que el fútbol rebote de lado a lado en el QWidget


**Ejercicio 22**

- Crear el siguiente método dentro de la clase AdminDB:

.. code-block:: c	
	
	/**
	 * @brief Método que ejecuta una consulta SQL a la base de datos que ya se encuentra conectado. 
	          Utiliza QSqlQuery para ejecutar la consulta, con el método next() se van extrayendo 
	          los registros que pueden ser analizados con QSqlRecord para conocer la cantidad de 
	          campos por registro.
	 * @param comando es una consulta como la siguiente: SELECT nombre, apellido, id FROM usuarios
	 * @return Devuelve un QVector donde cada elemento es un registro, donde cada uno de estos registros 
	           están almacenados en un QStringList que contiene cada campo de cada registro.	           
	 */
	QVector< QStringList > select( QString comando ); 

- Usarlo para consultar todos los logs que hay en la base.

**Ejercicio 23**

- Crear una clase Boton que hereda de QWidget
- Redefinir paintEvent en Boton y usar fillRect para dibujarlo de algún color
- Que cada Boton pueda tener un texto
- Que se pueda modificar el tamaño del texto
- Crear una botonera con varios objetos de Boton

**Ejercicio 24**

- Elegir un archivo de imagen del disco con ``QFileDialog`` y dibujar una grilla de 4 x 4 con copias de esta imagen
- Al hacer click sobre cada una de estas imágenes se deberá ocultar


**Ejercicio 25**

- Crear una clase base llamada Instrumento y las clases derivadas Guitarra, Bateria y Teclado.  
- La clase base tiene una función virtual pura llamada ``sonar()``. 
- Defina una función virtual ``verlo()`` que publique la marca del instrumento. Por defecto todos los instrumentos son de la marca Yamaha. 
- Utilice en la función ``main()`` un ``std::vector`` para almacenar punteros a objetos del tipo Instrumento. Instancie 5 objetos y agréguelos al ``std::vector``.
- Publique la marca de cada instrumento recorriendo el vector.
- En las clases derivadas agregue los datos miembro "``int cuerdas``", "``int teclas``" e "``int tambores``" según corresponda. Por defecto, guitarra con 6 cuerdas, teclado con 61 teclas y batería con 5 tambores.
- Haga que la clase ``Teclado`` tenga herencia múltiple, heredando además de una nueva clase ``Electrico``. Todos los equipos del tipo "``Electrico``" tienen por defecto un voltaje de 220 volts. Esta clase deberá tener un destructor que al destruirse publique la leyenda "Desenchufado".
- Al llamar a la función ``sonar()``, se deberá publicar "Guitarra suena...", "Teclado suena..." o "Batería suena..." según corresponda.
- Incluya los métodos ``get`` y ``set`` que crea convenientes.


Ejercicio Clase 21
==================

- Entregar al menos uno de estos ejercicios

Entregable Clase 21
===================

- Explicar en un video al menos un ejercicio
