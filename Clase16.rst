.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 16 - POO 2022
===================
(Fecha: 19 de mayo)


Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`MD5 independizar del SO 2021 <https://youtu.be/I4onYdM0Enk>`_

`Práctica con MD5 y base de datos 2021 <https://youtu.be/nLHdT_-8Afk>`_



Consulta a la base de datos
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	QSqlDatabase db = QSqlDatabase::addDatabase( "QSQLITE" );

	db.setDatabaseName( "C:/Qt/db/test" ); 

	if ( db.open() )  {
	    QSqlQuery query = db.exec( "SELECT nombre, apellido FROM usuarios" );

	    while( query.next() )  {
	        qDebug() << query.value( 0 ).toString() << " " << query.value( 1 ).toString();
	    }
	}

	


**Ejemplo**: slot de la clase Login para que valide usuarios contra la base

.. code-block:: c

	void Login::slot_validar()  {
	    bool usuarioValido = false;

	    if ( adminDB->getDB().isOpen() )  {  
	        QSqlQuery * query = new QSqlQuery( adminDB->getDB() );

	        query->exec( "SELECT nombre, apellido FROM usuarios WHERE usuario='" + 
	        leUsuario->text() + "' AND clave='" + leClave->text() + "'" );

	        // Si los datos son consistentes, devolverá un único registro.
	        while ( query->next() )  {

	            QSqlRecord record = query->record();

	            // Obtenemos el número de la columna de los datos que necesitamos.
	            int columnaNombre = record.indexOf( "nombre" );
	            int columnaApellido = record.indexOf( "apellido" );

	            // Obtenemos los valores de las columnas.
	            qDebug() << "Nombre=" << query->value( columnaNombre ).toString();
	            qDebug() << "Apellido=" << query->value( columnaApellido ).toString();

	            usuarioValido = true;
	        }

	        if ( usuarioValido )  {
	            QMessageBox::information( this, "Conexión exitosa", "Válido" );
	        }
	        else  {
	            QMessageBox::critical( this, "Sin permisos", "Usuario inválido" );
	        }
	    }
	}




Clase QCryptographicHash
^^^^^^^^^^^^^^^^^^^^^^^^

- Provee la generación de la clave hash 
- Soporta MD5, MD4 y SHA-1

.. code-block:: c

	enum Algorithm { Md4, Md5, Sha1 }

	QCryptographicHash(Algorithm metodo)

	void addData(const QByteArray & data)
	
	void reset()

	QByteArray result() const


**Método estático**

.. code-block:: c

	QByteArray hash( const QByteArray & data, Algorithm metodo )


**Otros métodos útiles**

.. code-block:: c

	QByteArray QByteArray::toHex()
	// Devuelve en hexadecimal
	// Útil para enviar por url una clave hash MD5
	// Hexadecimal tiene sólo caracteres válidos para URL

**Ejemplo**: Obtener MD5 de la clave ingresada en un QlineEdit:

.. code-block:: c

	QcryptographicHash::hash( leClave->text().toUtf8(), QCryptographicHash::Md5 ).toHex()
	


**Calculadora MD5 online**

http://www.md5.cz/



**Para independizar del SO**

.. code-block:: c

	AdminDB adminDB;
	QString nombreSqlite;

	#ifdef __APPLE__
	    nombreSqlite = "/home/cosimani/db/test";
	#elif __WIN32__
	    nombreSqlite = "C:/Qt/db/test";
	#elif __linux__
	    nombreSqlite = "/home/cosimani/db/test";
	#else
	    nombreSqlite = "/home/cosimani/db/test";
	#endif

	if ( adminDB.conectar( nombreSqlite ) )
	    qDebug() << "Conexion exitosa";


**Algunas explicaciones sobre base de datos** 


- `Crear base de datos <https://www.youtube.com/watch?v=U9iE6pM0bxM>`_

- `Crear tabla <https://www.youtube.com/watch?v=_-hKca2k784>`_

- `Insertar registro <https://www.youtube.com/watch?v=RggFhFZnCPU>`_

- `Consultar datos <https://www.youtube.com/watch?v=8emd37mvN2E>`_


Ejercicio Clase 16
==================

- Implementar el siguiente método de AdminDB en un proyecto que tenga un login y valide los usuarios contra la base de datos.
- La clave debe estar en MD5.
- Hacer los cambios necesarios en este método para su funcionalidad correcta.

.. code-block:: c	
	
	/**
	 * Si el usuario y clave son crrectas, este metodo devuelve el nombre y 
	 * apellido en un QStringList.	           
	 */
	QStringList AdminDB::validarUsuario( QString tabla,	QString usuario, QString clave )  {

	    QStringList datosPersonales;

	    if ( ! db.isOpen() ) 
	        return datosPersonales;

	    QSqlQuery * query = new QSqlQuery( db );
	    QString claveMd5 = QCryptographicHash::hash( clave.toUtf8(), 
	                                                 QCryptographicHash::Md5 ).toHex();

	    query->exec( "SELECT nombre, apellido FROM " +
	                 tabla + " WHERE usuario = '" + usuario +
	                 "' AND clave = '" + claveMd5 + "'" );
	
	    while( query->next() )  {
	        QSqlRecord registro = query->record();

	        datosPersonales << query->value( registro.indexOf( "nombre" ) ).toString();
	        datosPersonales << query->value( registro.indexOf( "apellido" ) ).toString();
	    }

	    return datosPersonales;
	} 



Entregable Clase 16
===================

- Punto de partida: Tener listo el Ejercicio Clase 16.
- Explicar línea por línea el método validarUsuario.








