.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 05 - POO 2022
===================
(Fecha: 1 de abril)


`Video con el contenido de esta Clase 05 POO 2022 <https://www.youtube.com/watch?v=7l0QZzqbQjI>`_


**¿ Cómo funciona el método getDatos() ?**


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



Convenciones para escribir nuestro código
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Los nombres de las clases, structs y enum comienzan con mayúsculas (usando ``UpperCamelCase``).
- Nombres de variables, funciones y métodos comienzan con minúsculas (usando ``lowerCamelCase`` y con palabras separadas con guión bajo).

- Ejemplos para nombres de clases: ``Persona`` - ``PrimeraClase`` - ``Ventana``
- Ejemplos para nombres de variables y funciones: ``velocidad`` - ``sumarNumeros`` - ``alto_imagen`` - ``anchoImagen``

**CamelCase**: Es escribir con la forma de jorobas de camello con las mayúsculas y minúsculas.

UpperCamelCase: La primera letra de cada palabra es mayúscula. Ejemplo: ``EjemploDeUpperCamelCase``.
lowerCamelCase: Igual a UpperCamelCase con excepción de la primer palabra. Ejemplo: ``ejemploDeLowerCamelCase``



Entregable Clase 05
===================

- Punto de partida: Empty qmake Project
- Crear una clase Jugador con atributos ``int velocidad``, ``int fuerza`` y ``std::string nombre``
- Usar constructor inicializando de la manera recomendada la velocidad en 0, fuerza en 0 y nombre "sin nombre" 
- Crear los métodos setter y getter para setear y obtener los valores de los atributos
- Incluir el destructor
- En la función main crear un ``std::vector< Jugador >`` e insertar 10 jugadores distintos
- Por último, publicar los datos de cada uno de los jugadores con ``std::cout``





