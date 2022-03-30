.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 04 - POO 2022
===================
(Fecha: 31 de marzo)


`Video con el contenido de esta Clase 04 POO 2022 <https://www.youtube.com/watch?v=dH0WqMW3-_w>`_


Clases
======

.. code-block:: c

	class Poste  {
	    // Lista de miembros (generalmente funciones y datos)
	    // Los datos no pueden ser inicializados fuera del constructor 
	    // Si las funciones se definen fuera, se usa el operador :: 
	    // :: es el operador de acceso a ámbito
	};


.. code-block:: c

	class Poste;  // Esto es la declaración de una clase.

.. code-block:: c

	class Poste  {  // Esto es la declaración y definición de una clase.
	     
	};




**Ejemplo:**

.. code-block:: c

	#include <iostream>
	
	class Poste  {
	private:
	    // Datos miembro de la clase Poste. También llamados atributos.
	    int altura;
	    int seccion;
		
	public:
	    // Funciones miembro de la clase Poste. Llamados también métodos.
	    void getDatos( int & a, int & s );
	    void setDatos( int a, int s )  {
	        altura = a;
	        seccion = s;
	    }
	};

	void Poste::getDatos( int & a, int & s )  {
	    a = altura;
	    s = seccion;
	}

	int main()  {
	    Poste poste;
	    int x, y;  // Variables donde se copiarán los valores de poste

	    poste.setDatos( 12, 32 );
	    poste.getDatos( x, y );

	    cout << "(" << x << “, ” << y << “)” << endl;
	}
	
	// La función "setDatos()" se definió en el interior de la clase (lo haremos sólo cuando
	// la definición sea muy simple, ya que dificulta la lectura y comprensión del programa). 

**Constructor**

.. code-block:: c

	class Poste  {
	private:
	    int altura;
	    int seccion;

	public:
	    Poste( int a, int s );

	    void getDatos( int & a, int & s );
	    void setDatos( int a, int s );
	};

	Poste::Poste( int a, int s )  {
	    altura = a;
	    seccion = s;
	}

	void Poste::getDatos( int & a, int & s )  {
	    a = altura;
	    s = seccion;
	}

	void Poste::setDatos( int a, int s )  {
	    altura = a;
	    seccion = s;
	}

**Cuestiones sobre declaraciones**

.. code-block:: c

	Poste poste;  // Llama al constructor sin parámetros. En esta última versión 
	              // de Poste, esto no serviría, ya que no hay constructor sin parámetros. 
	              // Si no se especifica un constructor, el compilador crea uno. 
	              // Por lo tanto, esta declaración sirve para una clase Poste 
	              // donde el programador no escriba constructor, o escriba uno sin recibir parámetros.

	Poste poste();  // Se entiende como el prototipo de una función sin parámetros que 
	                // devuelve un objeto Poste. Es decir, no sirve para instanciar un 
					// objeto con el contructor sin parámetros de Poste.

	Poste poste1( 12, 43 );  // Válido
	Poste poste2( 45, 34 );  // Válido


**Inicialización de objetos**

.. code-block:: c

	// Lo siguiente se permite y funciona casi siempre, (salvo cuando usemos const, que
	// veremos más adelante). Hay que tener presente que aquí, primero se reserva lugar 
	// en memoria para altura y seccion conteniendo basura y luego se le asignan los 
	// valores que vienen en los parámetros del constructor.
	Poste( int a, int s )  {
	    altura = a;
	    seccion = s;
	}

	// La siguiente sería la manera más correcta de inicializar los atributos de un 
	// objeto. En este caso, altura y seccion nunca contienen basura, sino que 
	// directamente se crean en memoria con el valor que vienen en los parámetros del constructor.
	Poste::Poste( int a, int s ) : altura( a ), seccion( s )  {  }

	Poste::Poste() : a( 0 ), b( 0 )  {  }

**El puntero this**

- Es un puntero que ya se exite dentro del ámbito de una clase y apunta al propio objeto instanciado.
- Se utiliza para acceder a los atributos y métodos.

.. code-block:: c

	class Poste  {
	private:
	    int altura;
	    int seccion;

	public:
	    Poste( int altura, int seccion );

	    void getDatos( int & altura, int & seccion );
	    void setDatos( int altura, int seccion );
	};

	Poste::Poste( int altura, int seccion ) : altura( altura ), seccion( seccion )  {  
	}

	void Poste::getDatos( int & altura, int & seccion )  {
	    altura = this->altura;
	    seccion = this->seccion;
	}

	void Poste::setDatos( int altura, int seccion )  {
	    this->altura = altura;
	    this->seccion = seccion;
	}


**Destructor**

.. code-block:: c

	Poste::~Poste()  {
	    altura = 0;  
	    seccion = 0;
	}
	

Entregable Clase 04
===================

- Punto de partida: Empty qmake Project
- Crear una nueva clase (que no sea Persona, ni Cliente, ni Poste)
- Agregar uno o más constructores, agregar sus métodos y sus atributos
- Utilizar la mayoría de los recursos que se utilizaron en el video de esta clase
- Crear algunos objetos de esta clase en la función main
