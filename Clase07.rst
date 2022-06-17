.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 07 - POO 2022
===================
(Fecha: 8 de abril)

Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`Help signal slot QSlider QSpinBox 2021 <https://www.youtube.com/watch?v=BHog8TPjnos>`_

Signals y slots
^^^^^^^^^^^^^^^

- signal y slot son funciones.
- Las signals de una clase se comunican con los slots de otra.
- Se deben conectar con la función connect de QObject.
- Un evento puede generar una signal.
- Los slots reciben estas signals.
- SIGNAL() y SLOT() son macros (convierten a cadena).
- emisor y receptor son punteros a QObject


.. code-block:: c

	QObject::connect( emisor, SIGNAL( signal ), receptor, SLOT( slot ) );
	
- Se puede remover la conexión:

.. code-block:: c

	QObject::disconnect( emisor, SIGNAL( signal ), receptor, SLOT( slot ) );

**Ejemplo:** QPushButton para cerrar la aplicación.

.. code-block:: c

	#include <QApplication>
	#include <QPushButton>

	int main( int argc, char** argv )  {
	    QApplication a( argc, argv );
	    QPushButton* boton = new QPushButton( "Salir" );

	    QObject::connect( boton, SIGNAL( pressed() ), &a, SLOT( quit() ) );
	    boton->setVisible( true );
		
	    return a.exec();
	}

	

**Ejercicio** 

- Crear una aplicación Qt que inicie con un botón que diga "Mostrar segundo boton y label"
- Al hacer clic sobre este botón se deberá ocultar este botón, se visualizará un nuevo botón y un label
- El segundo botón dirá "Ocultar label y mostrar boton final"
- Al hacer clic en el segundo botón, se ocultará este y el label, para mostrar el último botón
- El último botón dirá "Cerrar aplicacion" y cerrará la aplicación al presionarlo


Entregable Clase 07
===================

- Punto de partida: Entregable 06
- Teniendo el programa funcionando del entregable 6, modificarlo para que tenga el siguiente comportamiento
- Cuando inicie la aplicación, sólo el botón estará visible
- Al presionar el botón, se deberá visualizar el QLabel, el QWidget y el QLineEdit
- Cuando escribimos dentro del QLineEdit y se presiona Enter, en ese momento se deberá cerrar la aplicación
