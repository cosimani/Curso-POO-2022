.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 01 - POO 2022
===================
(Fecha: 17 de marzo)


:Autor: César Osimani
:Correo: cesarosimani@gmail.com

:Temas principales: 
		- Espacio de nombres
		- inline y const
		- std, vector, string
		- Aritmética de punteros
		- Funciones genéricas
		- Herencia y herencia múltiple
		- Polimorfismo
		- Funciones virtuales
		- Clases abstractas
		- Modificador friend
		- Biblioteca Qt
			- Uso de documentación
			- slots y signals
			- QtNetwork
			- Interfaz gráfica de usuario (widgets, layouts, etc.)
			- QPainter y captura de eventos del teclado y del mouse
			- QTimer
			- QtDesigner
		- OpenGL (glOrtho, gluPerspective, glLookAt, rotación, traslación, texturas, ...)
		- Base de datos (SELECT e INSERT).
		- Resolver los problemas consultando documentación técnica de distintas fuentes


Instalación de herramientas
===========================

:QtCreator: 
	- Desinstalar todas las versiones de Qt ejecutando C:\\Qt\\MaintenanceTool.exe y tildando Uninstall only 
	- Descargar el `Instalador Online <https://www.qt.io/download-thank-you?hsLang=en>`_
	- Ejecutar el archivo qt-unified-windows-x86-4.1.1-online.exe y utilizar una cuenta de Qt
	- Se recomienda: 'Qt 5.13.2'  Qt Creator 7.0.0-rc1'  'MinGW 7.3.0 32-bit'  'MinGW 7.3.0 64-bit'

:OpenSSL: 
	- Descargar instalador desde la `Página de descarga <https://slproweb.com/products/Win32OpenSSL.html>`_
	- Seleccionar el instalador .exe Win64 OpenSSL v1.1.1k 

:OBS Studio: 
	- Descargar instalador desde la `Página de descarga <https://obsproject.com/es>`_ e instalar


Metodología didáctica
=====================

- A continuación se resume el conjunto de estrategias, procedimientos y acciones para facilitar el aprendizaje y el logro de nuestros objetivos. 

:Teoría: 
	- En la primer parte de cada clase se expondrán los contenidos teóricos.

:Práctica: 
	- La segunda parte de cada clase estará destinado a la resolución de ejercicios.
	- El docente propone un ejercicio que, si los contenidos de la materia se mantienen al día, se pueden realizar durante la clase.
	- La búsqueda de la resolución del ejercicio se realiza de manera grupal en las mesas (de Discord) y la entrega es individual.
	- Luego de resolver el ejercicio se debe explicar, en un video compartiendo pantalla, cómo se resuelve y lo que se desee comentar.
	- Para cada ejercicio se definirá un "Punto de partida" que indicará desde dónde debe comenzar la explicación en el video.
	- Los ejecicios entregados correctamente llevan la nota 10 siempre que sea entregado hasta 24 horas posteriores a la finalización de la clase. Para los ejercicios de las clases que son los viernes, el tiempo de esta entrega el sigueinte día hábil hasta el mediodía.
	- Ejercicios no entregados llevan nota 0.
	- Los ejecicios entregados correctamente en un tiempo posterior de las 24 horas (o pasado el mediodía ...) la nota será un 5. 
	- En caso que pase más de una semana (aquí no se distinguen viernes de otro día) se considera como no entregado.
	- Ejercicios que no respeten el punto de partida y/o la completitud del ejercicio llevan nota 4.
	- Todo esto es válido para los que asistan a clases como para los que no. En caso de necesitar más tiempo por razones particulares, escribir al docente por WhatsApp para fijar una nueva hora de entrega.
	- El video debe quedar disponible en Youtube como No listado y se comparte el link por mensaje privado en Teams.
	- Para subir videos largo a Youtube, la cuenta debe estar verificada (`ver cómo hacerlo en este video: <https://www.youtube.com/watch?v=L2BZQlnlc5M>`_)
	- Denominaremos a estos ejercicios como Entregables.
	- El tiempo de duración del video queda a criterio de quien lo entrega.
	- El video se puede editar como se desee. (`aquí una herramienta online <https://online-video-cutter.com/es/>`_)
	- Entrar al siguiente `link para ver el registro de los entregables <https://docs.google.com/spreadsheets/d/1xbj6brqzdn3R9sfjDEP0LEjg6CwMNMOb8dBEYGmxhTw/edit?usp=sharing>`_ 


:Regularidad: 
	- Primer parcial: Trabajo práctico individual para resolver en 2 horas
	- Para este parcial se trabaja en equipo (por Discord en distintas Mesas) y se entrega individual ya que son exámenes distintos.
	- Segundo parcial: Promedio de todos los Entregables.
	- Recuperatorios: Se pueden recuperar ambos parciales durante la última semana de cursado. El recuperatorio del primer parcial es un práctico individual para resolver en 2 horas. El recuperatorio del segundo parcial tiene una parte práctica para resolver en 1 hora y una parte teórica para responder oralmente.


Entregable Clase 01
===================

- Punto de partida: Computadora sin Qt instalado
- Se pide grabar un video utilizando el Qt ejecutando un programa básica o de los ejemplos que ya trae el QtCreator.
- Este primer entregable tiene como objetivo poner a punto el mecanismo de entrega de los ejercicios de cada clase.
- Se recomienda: 'Qt 5.13.2'  'Qt Creator 7.0.0-rc1'  'MinGW 7.3.0 32-bit'  'MinGW 7.3.0 64-bit'  'OpenSSL 1.1.1j Toolkit'


