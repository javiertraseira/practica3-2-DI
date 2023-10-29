# Práctica 3.1 Usabilidad básica (guía de estilo) e instalación

## Parte 1

La práctica consiste en generar una **guía de estilo** y seguir algunas de las reglas básicas de **usabilidad** vistas, personalizando y reorganizando mediante paneles las ventanas de la aplicación desarrollada previamente:

-   Se deberá de utilizar *JPanels* sobre la ventana y como **layouts** el *Free Design* para la ventana principal y el *Null Layout* para los JPanels.
-   Se deberá hacer un estudio de la **usabilidad** de la aplicación (especialmente la parte de creación de usuarios nuevos), así como justificar el uso de una *paleta de colores* específica y una *fuente tipográfica*. Rellena el documento de la **guía de estilo** adjunto al proyecto.
-   La **barra superior** de las ventanas deberá de ser sustituida por barras personalizadas creadas por nosotros, que tengan su misma funcionalidad (excepto por el momento mover ventana).

   ![](media/3605716fc96796a96a8819be129560a7.png)


## Parte 2

Rediseña la **ventana principal**:
- Agrandándala y agrégale un gran panel central con un *JTextArea* y otro lateral con los botones. Agrega una barra inferior de estado con funcionalidad. 
- Agrega un menú superior con las opciones de **archivo** y **edición**.
	- El menú **archivo** tendrá la opción de abrir y guardar archivos de tipo texto cuyo contenido se cargará en el *JTextArea* central de la ventana principal.
	- Agrega un **selector de color** a las opciones del menú creado anteriormente, cuya función sea cambiar el color de fondo de los JPanel y de toda la interfaz.
![](media/9cd713b474093125d5571d49cd5b0243.png)

Mejora el ejercicio anterior permitiendo **mover** todas las ventanas desde su barra superior personalizada.

## Parte 3

Busca la forma de generar un **ejecutable** para *Windows_64* usando el fichero **jar** generado de tu proyecto. Agrégale un **icono** a tu aplicación.

Crea un **instalador** para tu aplicación usando el programa *installa4j* siguiendo los pasos del siguiente tutorial desde [este enlace.](https://www.raulprietofernandez.net/blog/programacion/como-crear-un-instalador-para-aplicaciones-java-con-install4j)

Opcional: Busca la forma de solventar el funcionamiento del gestor y la propia BD mediante el instalador.

Opcional: Busca la forma de mejorar el selector de color por defecto utilizado, ya sea en repositorios u otras clases en Internet. Haz lo mismo con el selector de ficheros por defecto.
