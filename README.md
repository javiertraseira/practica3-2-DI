# Práctica 3.1 Usabilidad básica (guía de estilo) e instalación

Esta práctica sirve como base de varios de los contenidos mínimos que debe cumplir el primer proyecto trimestral evaluable del módulo de Desarrollo de Interfaces.

## Parte 1

La práctica consiste en generar una **guía de estilo** rellenando un documento adjunto y seguir algunas de las reglas básicas de **usabilidad** vistas, personalizando y reorganizando el diseño, la barra superior y mediante paneles la aplicación desarrollada previamente para darle así un aspecto visual más acorde:

-   Se deberá hacer un estudio de la **usabilidad** de la aplicación (especialmente la parte de creación de usuarios nuevos), así como justificar el uso de una *paleta de colores* específica y una *fuente tipográfica*. Rellena el documento de la [guía de estilo](Plantilla_guia_de_estilo.md) adjunto al proyecto.
-   La **barra superior** de las ventanas deberá de ser sustituida por una barra personalizada creada por nosotros, con su misma funcionalidad (excepto por el momento mover la ventana). Nota: usar para ello la propiedad *undecorated* de un JFrame.
-   Se deberán de utilizar *JPanels* sobre la ventana y se recomienda utilizar como **layout** el *Free Design* para la ventana superior y el *Null Layout* para el panel principal.


   ![](media/3605716fc96796a96a8819be129560a7.png)


## Parte 2

Rediseña la **ventana principal** para que a partir de ahora se le añada contenido y funcionalidades:
- Crea un nuevo paquete llamado **media** donde almacenar todas las imágenes *png* o iconos que utilices en la aplicación a partir de ahora.
- Agrándala y agrégale un gran panel central con un *JTextArea* y otro lateral con los botones. Agrega una barra inferior de estado para darle funcionalidad y usabilidad. 
- Agrega un menú superior con las opciones de **archivo** y **edición**:
	- El menú **archivo** tendrá la opción de abrir y guardar archivos de tipo texto cuyo contenido se cargará en el *JTextArea* central de la ventana principal.
	- Agrega un **selector de color** a las opciones del menú de edición, cuya función sea cambiar el color de fondo de los *JPanel* y de toda la interfaz.
![](media/9cd713b474093125d5571d49cd5b0243.png)
- Mejora el ejercicio anterior permitiendo **mover** todas las ventanas desde su barra superior personalizada.

## Parte 3

Busca la forma de generar un **ejecutable** para *Windows_64* usando el fichero **jar** generado de tu proyecto usando la aplicación *Launch4J* o mediante el comando `jpackage` de Oracle. No te olvides de agregarle un **icono** propio a tu aplicación.

### Launch4J 

- Descarga e instala Launch4j.
- Crea un nuevo proyecto en Launch4j y especifica el archivo JAR de tu proyecto en la sección "Jar".
- Configura los parámetros que necesites, como la versión mínima de Java y el icono del ejecutable.
- Selecciona el archivo de salida (.exe) y guarda el proyecto.
- Haz clic en "Build wrapper" para generar el .exe.

Puede seguir los pasos desde el siguiente tutorial desde [este enlace.](https://www.raulprietofernandez.net/blog/programacion/como-crear-un-instalador-para-aplicaciones-java-con-install4j)


### Comando jpackage (Oracle)

- Asegúrate de tener la versión del JDK apropiada instalada. 
- Asegúrate de tener en la variable PATH la ruta a dicho comando para poder ejecutarlo.
- Ejecuta el siguiente comando desde la terminal en la carpeta del proyecto donde has generado el fichero JAR:
`jpackage --input ruta/al/jar --name NombreDeTuApp --main-jar TuArchivo.jar --main-class MainClass`


## Otras mejoras opcionales evaluable

Busca la forma de mejorar el selector de color por defecto utilizado, ya sea en repositorios u otras clases en Internet. Haz lo mismo con el selector de ficheros por defecto.

Investiga la forma de integrar el funcionamiento de la Base de Datos de tu aplicación mediante el instalador.

## Pruebas (testing)

| ID Caso Prueba | Descripción Caso de Prueba                                                                                               | Entrada esperada                                                                          | Salida esperada                                                                                      |
|----------------|--------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| 01             | Verificación de la paleta de colores y la fuente tipográfica aplicadas en la interfaz                                     | Colores y tipografía predefinidos en la guía de estilo                                     | Colores y fuente aplicados correctamente en todos los componentes                                      |
| 02             | Sustitución de la barra superior por una barra personalizada                                                             | Uso de `JFrame.setUndecorated(true)`                                                      | La barra superior personalizada aparece correctamente                                                 |
| 03             | Reorganización de la ventana principal usando `JPanel` con `Free Design` y `Null Layout`                                 | Uso de paneles organizados con los layouts indicados                                       | Paneles distribuidos correctamente según los layouts                                                   |
| 04             | Verificación del aumento de tamaño de la ventana principal con panel central y lateral                                   | Tamaño de ventana agrandado y paneles agregados                                            | Ventana principal correctamente redimensionada con los paneles añadidos                                |
| 05             | Añadir menú superior con opciones de "Archivo" y "Edición"                                                               | Menú añadido con opciones                                                                  | El menú superior con las opciones se muestra correctamente                                             |
| 06             | Funcionalidad para abrir y guardar archivos de texto desde el menú "Archivo"                                              | Archivo de texto seleccionado                                                             | Contenido del archivo cargado o guardado en el `JTextArea`                                              |
| 07             | Verificación de funcionalidad del selector de color en el menú "Edición"                                                  | Selección de un color en el selector                                                      | Color de fondo del `JPanel` y de la interfaz cambiado correctamente                                    |
| 08             | Mover las ventanas desde la barra superior personalizada                                                                 | Intento de mover la ventana desde la barra personalizada                                   | La ventana se puede mover desde la barra superior personalizada                                        |
| 09             | Generación de un ejecutable de Windows_64 con `Launch4J` o `jpackage`                                                      | Archivo `jar` del proyecto                                                                 | Ejecutable `.exe` generado correctamente                                                               |
| 10             | Creación de un instalador con Install4J                                                                                  | Configuración de un instalador para Windows                                                | Instalador generado que permite instalar la aplicación en Windows                                      |
| 11             | Mejora del selector de color predeterminado                                                                              | Uso de un selector de color personalizado                                                  | El nuevo selector de color reemplaza el predeterminado y ofrece más opciones                           |
| 12             | Mejora del selector de archivos predeterminado                                                                           | Uso de un selector de archivos personalizado                                               | El nuevo selector de archivos reemplaza el predeterminado y ofrece más funcionalidad                   |
| 13             | Integración de la Base de Datos en el instalador                                                                         | Configuración del instalador con los parámetros de la base de datos                        | La base de datos se integra y configura automáticamente durante la instalación                         |
| 14             | Estructura del proyecto                        | N/D   | Se utiliza la división por paquetes MVC; VistaControlador y Modelo para organizar las clases usando el modelo de objetos de forma apropiada | OK/No cumple|
| 15             | Comprobación fichero jar                        | Proyecto a empaquetar   | Se genera y prueba el fichero jar empaquetado | OK/No cumple|
| 16             | Creación de branches                        | -   | Se crean al menos dos branches en el repositorio github | OK/No cumple|
