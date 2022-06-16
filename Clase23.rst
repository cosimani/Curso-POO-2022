.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 23 - POO 2022
===================
(Fecha: 16 de junio)


Levantar base de datos a QTableView
===================================

- Colocar con el QtDesigner un QTableView

.. code-block:: c

	QSqlRelationalTableModel * tableModelAlumnos;
	tableModelAlumnos = new QSqlRelationalTableModel( this, adminDB->getDB() ); 

	tableModelAlumnos->setTable( "alumnos" );  // Tabla de la base

	// Para modificar como una planilla de excel
	tableModelAlumnos->setEditStrategy( QSqlTableModel::OnManualSubmit ); 

	// Otra relación. En lugar de mostrar el id_carrera que muestre el nombre de la carrera.
	tableModelAlumnos->setRelation( 5, QSqlRelation( "carreras", "id", "nombre" ) );

	tableModelAlumnos->select();  // Hace la consulta.

	// Títulos de las columnas en el widget.
	tableModelAlumnos->setHeaderData( 1, Qt::Horizontal, "Legajo" );
	tableModelAlumnos->setHeaderData( 2, Qt::Horizontal, "Nombre" );
	tableModelAlumnos->setHeaderData( 3, Qt::Horizontal, "Apellido" );
	tableModelAlumnos->setHeaderData( 4, Qt::Horizontal, "Mail" );
	tableModelAlumnos->setHeaderData( 5, Qt::Horizontal, "Carrera" ); 

	// Seteamos el QSqlTableModel sobre el QTableView
	ui->tableViewAlumnos->setModel( tableModelAlumnos );

	// Lista desplegable con el nombre de la carrera, esto cuando se modifique la celda.
	ui->tableViewAlumnos->setItemDelegate( new QSqlRelationalDelegate( ui->tableViewAlumnos ) );

	// Ocultamos la columna id de la tabla alumnos.
	ui->tableViewAlumnos->setColumnHidden( 0, true );

	// Ajusta el ancho de la celda con el texto en su interior. Para todas las columnas.
	ui->tableViewAlumnos->resizeColumnsToContents(); 
	
.. code-block:: c

	void Principal::slot_guardarCambios()  {    // Guada todos los cambios 
	    tableModelAlumnos->submitAll();
	}

	void Principal::slot_deshacer()  {  // Deshace todos los cambios que hizo el usuario.
	    tableModelAlumnos->revertAll();
	}
		

Creación de tablas
------------------

.. code-block:: c

	CREATE TABLE 'carreras' ('id' INTEGER PRIMARY KEY AUTOINCREMENT, 'nombre' VARCHAR)

	CREATE TABLE 'alumnos' ( 'id' INTEGER PRIMARY KEY AUTOINCREMENT, 
	                         id_carrera integer, 'nombre' VARCHAR, 
	                         'apellido' VARCHAR, 'mail' VARCHAR, 'legajo' VARCHAR, 
	                         foreign key(id_carrera) references carreras(id) )


Para rendir el final de POO
===========================

:Opción Desafíos:
	- Corresponde un 50% para un desafío y el otro 50% para la pregunta sobre `Temas 1 al 10 de los vistos en clase <https://github.com/cosimani/Curso-POO-2022/blob/main/Desafios.rst>`_
	- La pregunta sobre los temas pueden ser respondidas de manera oral, explicadas con alguna presentación y/o explicadas miestras se escribe código.
	- Para la pregunta sobre los temas se puede pedir desarrollo de código.

:Opción TP:
	- Para realizar la entrega en una fecha de examen, primero debe ser aprobada con, al menos, 48 horas antes del examen.
	- Para ser aprobada debe tener un mínimo del 70% de la totalidad (70% corresponde a la nota 6 en la escala que se utiliza para los finales).
	- El trabajo debe tener los contenidos vistos en clases (`Temas 1 al 10 <https://github.com/cosimani/Curso-POO-2022/blob/main/Desafios.rst>`_).
	- Si el trabajo no está al 100%, se preguntará sobre los temas 1 al 10 y/o se pedirán modificaciones sobre el trabajo durante la hora del examen.
	- La presentación del trabajo se realiza de forma oral y de manera individual.


Ejercicio Clase 23
==================

- Hacer funcionar un QTableView mostrando la tabla usuarios y su relación con otra tabla
- Tabla alumnos: id, legajo, nombre, apellido, mail, id_carrera
- Tabla carreras: id, nombre
- Usar QtDesigner

Entregable Clase 23
===================

- Explicar el ejercicio en un video.
