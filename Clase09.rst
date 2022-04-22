.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 09 - POO 2022
===================
(Fecha: 22 de abril)


Dibujar a mano sobre un QWidget
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	// mapa.h
	#include <QWidget>

	class Mapa : public QWidget  {
	    Q_OBJECT

	public:
	    Mapa()  {  }

	protected:
	    void paintEvent( QPaintEvent * );

	};

	// mapa.cpp
	#include "mapa.h"
	#include <QPainter>

	void Mapa::paintEvent( QPaintEvent * )  {
	    QPainter painter( this );
	    painter.drawLine( 0, 0, this->width(), this->height() );
	}

**Clase QPainter**

- Pinta a bajo nivel sobre widgets.
- Debe ser utilizado dentro del método ``paintEvent( QPaintEvent * )``.

.. code-block:: c

	void drawEllipse( int x, int y, int ancho, int alto )
	void drawImage( int x, int y, QImage & image )
	void drawLine( int x1, int y1, int x2, int y2 )
	void drawText( int x, int y, QString & text )
	void fillRect( int x, int y, int ancho, int alto )



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


QGridLayout
^^^^^^^^^^^

- Ubica los widgets en una grilla
- Con setColumnMinimumWidth() podemos setear el ancho mínimo de columna
- Separación entre widget con setVerticalSpacing( int )
- void addWidget( QWidget * widget, int fila, int columna, int spanFila, int spanCol )



Ejercicio Clase 09
==================

- Construir un login.
- Usar asteriscos para la clave.
- Detectar enter para simular la pulsación del botón.
- Si la clave ingresada es admin:admin, la aplicación se cerrará.
- Si se ingresa otra clave se borrará el texto de los QLineEdit.

- Tener en cuenta que este ejercicio requiere conocer cómo se define un slot propio.


Entregable Clase 09
===================

- Punto de partida: Proyecto vacío
- Explicar a medida que va escribiendo código, la creación de un QGridLayout para un login 
- También se puede ir explicar con voz en off




