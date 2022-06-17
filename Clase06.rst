.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 06 - POO 2022
===================
(Fecha: 7 de abril)

Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`Introducción a Qt 2021 <https://www.youtube.com/watch?v=JYADonAlKPc>`_

`Primer aplicación en Qt 2021 <https://www.youtube.com/watch?v=krfWC8mWTQM>`_


Primer aplicación en Qt con interfaz gráfica
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Qt(Quasar Toolkit) 
	- Biblioteca para desarrollo de software de Quasar Technologies
	- Se llamó también Trolltech
	- Biblioteca multiplataforma
	- En el 2008 lo compró Nokia
	- Aplicaciones escritas con C++ (Qt)
		- KDE
		- VLC Media Player
		- Skype
		- VirtualBox
		- Google Earth 
		- Spotify para Linux
	- En 2012, Digia compra Qt y comercializa las licencias 
	- Digia desarrolló herramientas para usar Qt en iOS y Android.
		

**Ejemplo**

- Creación de una aplicación Qt

.. code-block:: c

	#include <QApplication>	
	// - Administra los controles de la interfaz
	// - Procesa los eventos
	// - Existe una única instancia
	// - Analiza los argumentos de la línea de comandos

	int main( int argc, char** argv )  {	
	    // app es la instancia y se le pasa los parámetros de la línea
	    // de comandos para que los procese.
	    QApplication app( argc, argv ); 

	    QLabel hola( "<H1 aling=right> Hola </H1>" );
	    hola.resize( 200, 100 );
	    hola.setVisible( true );

	    app.exec();  // Se le pasa el control a Qt
	    return 0;
	}



Entregable Clase 06
===================

- Punto de partida: Empty qmake Project
- En la función main crear un objeto de la clase QLabel, uno de QWidget, uno de QPushButton y uno de QLineEdit
- Invocar al método show() de cada uno de estos 4 objetos
- Cada objeto se mostrará independiente y con esto termina el entregable