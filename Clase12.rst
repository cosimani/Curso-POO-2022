.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 12 - POO 2022
===================
(Fecha: 5 de mayo)

Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`Dibujar a mano - QByteArray - Preprocesador 2021 <https://www.youtube.com/watch?v=8Gu5_ejipus>`_

`Derivadas - Constructor explícito 2021 <https://www.youtube.com/watch?v=O2mCsBB_gro>`_






:Videos recomendados:
	Ver `Tutorial Qt QVector <https://www.youtube.com/watch?v=Z9u2yDPh57U>`_ de `Videos tutoriales de Qt <https://www.youtube.com/playlist?list=PL54fdmMKYUJvn4dAvziRopztp47tBRNum>`_

	Ver `Tutorial Qt QDateTime <https://www.youtube.com/watch?v=bZmGhmKv5iE>`_ de `Videos tutoriales de Qt <https://www.youtube.com/playlist?list=PL54fdmMKYUJvn4dAvziRopztp47tBRNum>`_

	Ver `Tutorial Qt signals & slots <https://www.youtube.com/watch?v=IITGountoO4>`_ de `Videos tutoriales de Qt <https://www.youtube.com/playlist?list=PL54fdmMKYUJvn4dAvziRopztp47tBRNum>`_





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




Clases derivadas 
^^^^^^^^^^^^^^^^

.. code-block:: c
 
	// personal.h
	#include <QString>

	class Personal  {
	public:
	    QString verEdad()  {  return "Edad: " + QString::number( edad );  }
	    QString verSalario()  {  return "Salario: " + QString::number( salario );  }

	protected:  // Para acceso desde las clases derivadas
	    int edad;
	    int salario;
	};

	// Modificadores de acceso para Herencia:
	//    public  ->  Mantiene los modificadores de acceso de la clase base
	//    private ->  Pasa todo a privado
	class Desarrollador : public Personal  {
	public:
	    Desarrollador( int edad )  {
	    salario = 2000;
	    this->edad = edad;
	}

	// Se podrá usar? 
	Desarrollador( int edad ) : salario( 2000 ), edad( edad )  {  }
	    // No. Sólo para miembros de la propia clase (no para heredados).
	};

	class Administrador : public Personal  {
	public:
	    Administrador()  {
	        salario = 2000;
	        edad = 30;
	    }
	};

	#include <QApplication>
	#include "personal.h"
	#include <QDebug>

	int main( int argc, char ** argv )  {
	    QApplication a( argc, argv );

	    Desarrollador juan( 20 );
	    Administrador marcos;

	    qDebug() << juan.verEdad();
	    qDebug() << juan.verSalario();

	    qDebug() << marcos.verEdad();
	    qDebug() << marcos.verSalario();

	    return a.exec();
	}

Constructor de la clase derivada
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	class Persona  {
	public:
	    Persona( int edad ) : edad( edad )  {  }
	    QString verEdad()  {  return "Edad: " + QString::number( edad );  }
	    void setEdad( int edad )  {  this->edad = edad;  }

	protected:
	    int edad;
	};

	class Empleado : public Persona  {
	public:
	    // Siempre primero se llama al constructor de la clase base
	    Empleado( int edad, int salario ) : Persona( edad ), salario( salario )  {  }
	    QString verSalario()  {  return "Salario: " + QString::number( salario );  }

	protected:
	    int salario;
	};

	#include <QApplication>
	#include "personal.h"
	#include <QDebug>

	int main( int argc, char ** argv )  {
	    QApplication a( argc, argv );

	    Persona carlos( 24 );
	    Empleado ale( 20, 2500 );

	    qDebug() << carlos.verEdad();
	    //    qDebug() << carlos.verSalario();  // No compila. No está en la clase base.

	    qDebug() << ale.verEdad();
	    qDebug() << ale.verSalario();

	    return a.exec();
	}



Destructor de la clase derivada
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	class ClaseA  {
	public:
	    ClaseA() : datoA(10)  {  qDebug() << "Constructor A";  }
	    ~ClaseA()  {  qDebug() << "Destructor A";  }
	    int verA()  {  return datoA;  }

	protected:
	    int datoA;
	};

	class ClaseB : public ClaseA  {
	public:
	    ClaseB() : datoB( 20 )  {  qDebug() << "Constructor B";  }
	    ~ClaseB()  {  qDebug() << "Destructor B";  }
	    int verB()  {  return datoB;  }

	protected:
	    int datoB;
	};

	#include <QApplication>
	#include "personal.h"
	#include <QDebug>

	int main( int argc, char ** argv )  {
	    QApplication a( argc, argv );

	    {
	    ClaseB objeto;
	    qDebug() << "a=" << objeto.verA() << ", b=" << objeto.verB();
	    }

	    return a.exec();
	}

	// Publica
	Constructor A
	Constructor B
	a=10, b=20
	Destructor B
	Destructor A



Constructor explícito
^^^^^^^^^^^^^^^^^^^^^

- En el siguiente ejemplo tenemos una clase con un constructor no explícito:

.. code-block:: c

	class Persona  {
	private:
	    int edad;

	public:
	    Persona( int edad = 0 ) : edad( edad )  {  }

	    int getEdad()  {  return edad;  }
	    void setEdad( int edad )  {  this->edad = edad;  }   
	};

- Lo que permite instanciar objetos de todas las siguientes maneras:

.. code-block:: c

	Persona carlos;
	Persona miguel( 25 );
	Persona * roman = new Persona;
	Persona * juan = new Persona( 18 );

	Persona roberto = 23;

- Llama la atención la última de las maneras. 
- En ese caso, el compilador permite la conversión, ya que se entiende que el programador quiere usar el constructor que recibe un int como parámetro.

- Si deseamos bloquear esta posibilidad, debemos indicar que el constructor sea explícito, de la siguiente manera:

.. code-block:: c

	class Persona  {
	private:
	    int edad;

	public:
	    explicit Persona( int edad = 0 ) : edad( edad )  {  }

	    int getEdad()  {  return edad;  }
	    void setEdad( int edad )  {  this->edad = edad;  }   
	};

- Cuando un constructor no explícito recibe dos variables:

.. code-block:: c

	class Persona  {
	private:
	    int edad;
	    int dni;

	public:
	    Persona( int edad = 0, int dni = 0 ) : edad( edad ), dni( dni )  {  }

	    int getEdad()  {  return edad;  }
	    void setEdad( int edad )  {  this->edad = edad;  }
	    int getDni()  {  return dni;  }
	    void setDni( int dni )  {  this->dni = dni;  }
	};

- Se puede hacer lo siguiente:

.. code-block:: c

	Persona roberto = { 23, 35876543 };

- Y tener en cuenta que también es posible lo siguiente:

.. code-block:: c

	// Cuando el constructor recibe 3 parámetros y de distintos tipos
	Persona( int edad = 0, int dni = 0, QString nombre = "" ) : edad( edad ),
	                                                            dni( dni ), 
	                                                            nombre( nombre )  {  
	}

	// Se puede instanciar un objeto así:
	Persona roberto = { 23, 35876543, "Roberto" };

- A continuación un ejemplo por Carlos Duarte para `Constructor explícito <https://www.youtube.com/watch?v=lsdC3F27lt0>`_



Ejercicio Clase 12
==================

- Crear la jerarquía de clases en donde la clase Persona sea la clase base.
- Cliente y Administrativo derivan de Persona.
- Oro y Platino heredan de Cliente.
- Coloque las características más comunes que deberían tener estas clases.
- La aplicación deberá crear un cliente Platino con las características que vienen desde consola.
- Ejecutar la aplicación por consola pasando los siguientes parámetros obligatorios:
- nombreCliente edad numeroLegajo cantidadTarjetas montoAlDescubierto


Entregable Clase 12
===================

- Punto de partida: Proyecto vacío
- Explicar constructor explícito y programar algunos ejemplos distintos a los vistos en clase.


 