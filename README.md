# Práctica 3.1 Guía de estilo aplicación

## Parte 1

La práctica consiste en utilizando una **guía de estilo** y siguiendo reglas de **usabilidad** vistas, personalizar mediante paneles las ventanas de la aplicación desarrollada previamente:
-   Se deberá de utilizar *JPanels* sobre la ventana y como **layouts** el *Free Design* para la ventana principal y el *Null Layout* para los JPanels.
-   Se deberá hacer un estudio de la *paleta de colores* específica y justificar su uso así como el de la *tipografía* usada. Rellena el documento de la **guía de estilo** adjunto al proyecto.
-   La **barra superior** de las ventanas deberá de ser sustituida por barras personalizadas creadas por nosotros, que tengan su misma funcionalidad (excepto por el momento mover ventana)

    ![](media/840647d950380324a5c3ae3b8fdee5f3.png)
    ![](media/3605716fc96796a96a8819be129560a7.png)


## Parte 2

Mejora el ejercicio anterior permitiendo **mover** todas las ventanas desde su *JPanel* personalizado.

Rediseña la **ventana principal**:

- Agrandándala y agrégale un gran panel central con un *TextArea* y otro lateral con los botones. Agrega una barra inferior de estado con funcionalidad. 
- Agrega un menú superior con las opciones de **archivo** y **edición**.
	- El menú archivo tendrá la opción de abrir y guardar archivos de tipo texto cuyo contenido se cargará en el TextArea central de la ventana principal.
	- Agrega un **selector de color** a las opciones del menú creado anteriormente, cuya función sea cambiar el color de fondo de los JPanel y de toda la interfaz.

![](media/9cd713b474093125d5571d49cd5b0243.png)

## Parte 3

Empaqueta debidamente tu aplicación en un solo fichero jar. Busca la forma de generar un **ejecutable** para *Windows_64*.  Agrégale un **icono** a tu aplicación.

Opcional: Busca la forma de mejorar el selector de color por defecto utilizado, ya sea en repositorios u otras clases en Internet. Haz lo mismo con el el selector de ficheros por defecto.
