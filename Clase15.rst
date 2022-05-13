.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 15 - POO 2022
===================
(Fecha: 13 de mayo)


Conexión a base de datos
^^^^^^^^^^^^^^^^^^^^^^^^

**Ejemplo de la estructura de las tablas en la base de datos**

.. figure:: imagenes/tablas.png 

- Con Qt se pueden utilizar los siguientes motores de base de datos:
	- **ODBC (Open DataBase Connectivity)**: 
		- Estándar de acceso a base de datos
		- Usado con Microsoft Access en Windows
		- Está disponible en Windows: Panel de control -> Herramientas administrativas -> ODBC Data sources
			
	- **SQLite**
		- Es un sistema de gestión de bases de datos relacional.
		- En C y libre
		- Los datos se almacenan en un archivo
		- No es cliente-servidor. La librería (dll) tiene funciones para trabajar
		- No requiere instalación, directamente con un ejecutable
		- Para Linux, Windows, Mac OS, Android, iOS, BlackBerry OS, Windows Phone, ...
		- Algunas aplicaciones que usan SQLite: Skype, Firefox, Photoshop, ...
			
	- **MySQL**
		- Quizás el motor de base de datos más utilizado
		- Usado por los más grandes: Facebook, Twitter, YouTube, Wikipedia, ...
		- Requiere una instalación más avanzada para usar con Qt dependiendo el SO que se utilice.
		
Usando SQLite
^^^^^^^^^^^^^

**Creación de una base de datos SQLite**
	
- Descargar de http://www.sqlite.org/download.html
- Precompiled Binaries for Windows–Linux–MAC (The command-line shell program)
- En Linux se puede hacer: ``sudo apt-get install sqlite3``
- Al descomprimir tenemos el ejecutable sqlite3
- Creamos una carpeta C:/Qt/db (o /home/db) y copiamos ahí el ejecutable
- En consola creamos una base de datos, por ejemplo, llamada ``test`` con una tabla ``usuarios``

::

	sqlite3 test

	create table usuarios (
	    id integer primary key,  (es autoincrementable)
	    usuario varchar(30),
	    clave varchar(30),
	    nombre varchar(50),
	    apellido varchar(50),
	    mail varchar(50)
	);

	// Podemos insertar un registro 

	insert into usuarios (usuario, clave,	nombre, apellido, mail) 
	values ("cgomez", "1234", "Carlos", "Gomez", "cgomez@gmail.com");

	// Podemos ver el contenido de la tabla "usuario":

	select * from usuarios;

	// Para salir de la base:
		
	.exit

En Qt	
^^^^^

- Requiere QT += sql
- Para averiguar los controladores disponibles, usamos el método estático:

.. code-block:: c

	qDebug() << QSqlDatabase::drivers();  // Devuelve un QStringList

- Un objeto QSqlDatabase representa la conexión a la base
- Elegimos el controlador y conectamos:

.. code-block:: c

	QSqlDatabase db = QSqlDatabase::addDatabase( "QSQLITE" );

	db.setDatabaseName( "C:/Qt/db/test" ); 
	if ( db.open() )
	    qDebug() << "Conexión exitosa";
	else
	    qDebug() << "No se pudo abrir la base";

- En Windows, para usar el archivo Access ``C:/db/base.mdb`` se hace lo siguiente:
	
.. code-block:: c
		
	QSqlDatabase db = QSqlDatabase::addDatabase( "QODBC" );

	db.setDatabaseName( "DRIVER={Microsoft Access Driver (*.mdb, *.accdb)};"
	                    "DBQ=C:/db/base.mdb" ); 
	if ( db.open() )
		qDebug() << "Conexión exitosa";



**Preparando la clase AdminDB**

- Definir una clase AdminDB para administrar la base de datos
- Crear el siguiente método:

.. code-block:: c
	
	bool conectar(QString archivoSqlite); 

- En un proyecto nuevo y desde la función main() intentar la conexión.

.. code-block:: c

	// --- adminDB.h ---------------
	#include <QSqlDatabase>
	#include <QString>
	#include <QObject>

	class AdminDB : public QObject  {
	    Q_OBJECT

	public:
	    AdminDB();
	    bool conectar( QString archivoSqlite );
	    QSqlDatabase getDB();

	private:
	    QSqlDatabase db;
	};

	// --- adminDB.cpp ------------
	#include "adminDB.h"

	AdminDB::AdminDB()  {
	    db = QSqlDatabase::addDatabase( "QSQLITE" );
	}

	bool AdminDB::conectar( QString archivoSqlite )  {
	    db.setDatabaseName( archivoSqlite );

	    if( db.open() )
	        return true;

	    return false;
	}

	QSqlDatabase AdminDB::getDB()  {
	    return db;
	}

	// --- main.cpp  ----------------
	#include <QApplication>
	#include "adminDB.h"

	int main( int argc, char** argv )  {
	    QApplication a( argc, argv );

	    qDebug() << QDir::currentPath();

	    AdminDB adminDB;
	    if (adminDB.conectar( "C:/Qt/db/test" ) )
	        qDebug() << "Conexion exitosa";
	    else
	        qDebug() << "Conexion NO exitosa";

	return 0;
	}


Práctica Clase 15
=================

- Esta actividad correponde es un ejercicio en el cual se entrega el código fuente por Teams y tiene validez por el Ejercicio o Entregable de esta clase. Es de entrega obligatoria, lleva una nota de acuerdo a cómo haya sido resuelto y la fecha máxima de entrega es de una semana. En caso de no entregar, se deberá recuperar en la semana de recuperatorio.
- Buscar el correspondiente valor de User-Agent para un navegador en Android y otro para PC
- Realizar una interfaz que permita colocar en un ``QLineEdit`` la url de una página web
- Validar que si el usuario no escribe el www, que lo agregue, y si no coloca https://, que lo agregue
- Realizar dos consultas a varias páginas web con ambos valores de User-Agent
- Mostrar en dos ``QTextEdit`` el código fuente de ambas páginas
- Comparar si los códigos son iguales y que un ``QLabel`` muestre "Iguales" o "Distintos" según corresponda