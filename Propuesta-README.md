# Práctica 3.2. Rediseño y entrega de una aplicación de escritorio

Convierte la aplicación de login y registro de la **práctica 3.1** en un pequeño proyecto de escritorio que puedas entregar y defender. Elige un contexto de uso, aplica tu propia **guía de estilo** y amplía la ventana principal con un directorio de datos y un espacio para editar notas.

El proyecto integra lo trabajado en la **UT3.1**, sobre usabilidad y diseño de interfaces, y en la **UT3.2**, sobre acceso a datos mediante JDBC. Mantendrás Java Swing, FlatLaf y MySQL en Aiven.

## Preparación del proyecto

1. Crea el proyecto Maven `SOL/practica3-2` a partir de una versión funcional de la 3.1. Utiliza Java 21 y conserva los formularios de NetBeans, los recursos y las pruebas.
2. Mantén la separación **Modelo–VistaControlador** que utilizaste en la práctica anterior. Las ventanas recogen datos y muestran resultados. El modelo valida y realiza las operaciones sobre la base de datos.
3. Reutiliza el servicio MySQL de Aiven y el esquema de prácticas. Trabaja con cuentas, nombres y correos ficticios.
4. Utiliza las ramas `parte-1`, `parte-2` y `parte-3`. Integra cada parte comprobada en `main`, realiza commits descriptivos y registra en Issues los fallos que encuentres y su resolución.

### Elige el contexto de uso

Antes de diseñar, escribe un breve planteamiento con el **nombre de la aplicación**, a quién va dirigida y qué tareas va a facilitar. Por ejemplo, un club puede consultar a sus socios y guardar notas de actividades. Un aula puede consultar sus cuentas de demostración y preparar avisos.

El contexto debe reflejarse en los nombres de las secciones, en los datos de ejemplo y en al menos una decisión de diseño. **Implementa los requisitos comunes y elige una mejora propia** que tenga sentido para las personas que usarían la aplicación.

## Parte 1. Diseño, registro y configuración

### Guía de estilo

Crea `docs/guia-de-estilo.md`. Si el repositorio proporciona una plantilla, puedes utilizarla como punto de partida. Incluye:

- Paleta con sus valores y el uso previsto de cada color, tanto en tema claro como oscuro.
- Tipografía, tamaños y jerarquía para títulos, texto y controles.
- Icono de la aplicación, estilo de los botones, márgenes y alineación.
- Aspecto del foco, la selección y los estados de carga, error y confirmación.
- Boceto de la ventana principal y **tres decisiones justificadas** con criterios de la unidad. Indica qué tarea mejora cada decisión.

Aplica la guía al login, al registro y a la ventana principal. Comprueba que la interfaz se recorre con **Tab** y que los mensajes se entienden por su texto. Guarda los iconos que utilices en los recursos del proyecto Maven, de forma que se carguen también desde el JAR.

### Mejora de la ventana de registro

Conserva las reglas de la 3.1 para usuario, contraseña, confirmación y cuentas duplicadas. Añade validación a los datos opcionales **cuando tengan contenido**:

| Campo | Comprobación |
|---|---|
| Nombre y apellidos | Dales una longitud mínima y máxima.  |
| Correo electrónico | Comprueba que tiene una estructura básica válida y que no contiene espacios. |
| Fecha de nacimiento | Utiliza un selector visual, como `JDateChooser`, y permite borrar la selección. Admite una fecha válida igual o anterior a la fecha actual. |

Para el `JDateChooser` has de agregar la dependencia adecuada en el pom.xml y posteriormente también agregar dicho al editor de Apache Netbean mediante el *Palette Manager*.

Puedes dejar en blanco todos los datos opcionales. Guarda los datos válidos asociados a la cuenta, con la fecha como dato de tipo `DATE`. Centraliza las reglas en `ValidadorUsuario` y presenta los errores junto al formulario, indicando qué debe corregirse.

### Conexión a Aiven desde un fichero externo

En la 3.1 los valores de conexión estaban en `ConexionBD`. En esta práctica, esa clase los obtendrá de un fichero externo `config.properties` mediante `Properties`.

Entrega un `config.properties.example` con valores ficticios:

```properties
db.url=jdbc:mysql://HOST_AIVEN:PUERTO_AIVEN/usuarios
db.user=USUARIO_MYSQL
db.password=CONTRASENA_MYSQL
```

Cada estudiante creará su copia local. Elige y documenta una forma reproducible de localizarla, por ejemplo, una ruta dentro de la carpeta personal o un selector de archivo. Debe funcionar desde **NetBeans, el JAR y el ejecutable**. Deja el fichero privado fuera del JAR y del repositorio. Si falta o está incompleto, muestra un mensaje que indique cómo configurarlo y permite volver a intentarlo.

## Parte 2. Ventana principal y mejora propia

### Distribución y navegación

Organiza la ventana principal en dos zonas. Un **panel lateral** identifica la aplicación y permite cambiar de sección. El **área de trabajo** muestra el título, las acciones y el contenido de la sección activa. Reserva espacio para mensajes como «Cargando directorio», «Archivo guardado» o «Hay cambios sin guardar».

![Maqueta de Club Atlas. La navegación lateral da acceso a Directorio, Notas y Preferencias. El área central muestra una tabla de usuarios, la opción Actualizar y un buscador de ejemplo.](media/ventana-principal-club-atlas.png)

*Maqueta orientativa. El buscador es un ejemplo de mejora propia. Cada proyecto puede elegir su identidad visual y sus nombres de sección.*

En Swing puedes construir la pantalla con un `JPanel` lateral y un panel central con `CardLayout` para alternar las vistas. También puedes conservar un `JTabbedPane` si encaja en tu diseño. Marca la sección activa, mantén las acciones de cuenta en una ubicación previsible y comprueba que el contenido sigue siendo legible al redimensionar.

### Directorio con datos de Aiven

- Carga desde MySQL los registros del directorio en un `JTable` de consulta, con encabezados comprensibles y una acción **Actualizar**. Puedes reutilizar `usuarios` e `info` y elegir las columnas adecuadas para tu contexto. Incluye las cuentas que carezcan de información opcional.
- Selecciona en SQL únicamente las columnas que necesite la tabla. Mantén las contraseñas y demás datos de autenticación fuera de la consulta del directorio.
- Distingue los estados **cargando**, **sin registros** y **error de conexión**. Utiliza `PreparedStatement` en operaciones con parámetros y `try-with-resources` para liberar los recursos JDBC.

### Notas con archivos de texto

- Incluye un `JTextArea` editable dentro de un `JScrollPane`. Permite **Abrir** y **Guardar** archivos de texto con `JFileChooser`, desde el menú **Archivo** o desde acciones visibles de la sección.
- Lee y guarda en **UTF-8**. Muestra el nombre del archivo y señala cuándo existen cambios pendientes.
- Al abrir otro archivo, cerrar sesión o salir con cambios pendientes, ofrece guardar, descartar o cancelar. Si se cancela o falla el guardado, conserva el texto. Pide confirmación antes de sobrescribir otro archivo existente.

### Cuenta y preferencias

- Identifica al usuario que ha iniciado sesión y mantén disponible **Cerrar sesión**.
- Permite **Cambiar contraseña** desde una ventana o diálogo. Solicita la contraseña actual, la nueva y su confirmación. Reutiliza la validación del registro y modifica únicamente la cuenta de la sesión. Tras el cambio, la nueva contraseña debe permitir iniciar sesión y la anterior debe rechazarse.
- Permite alternar entre **tema claro y oscuro** con FlatLaf. Comprueba la legibilidad y el aspecto de las ventanas y diálogos al cambiar de tema.

### Mejora propia

Implementa **una** mejora que resuelva una necesidad de tu contexto. Puedes elegir una de estas propuestas o plantear otra de alcance parecido:

| Idea | Ejemplo |
|---|---|
| Localizar registros | Filtrar el directorio por nombre o usuario. |
| Agilizar tareas frecuentes | Añadir una barra de herramientas o un menú contextual al editor. Reutiliza las acciones que ya existen. |
| Adaptar la lectura | Elegir un tamaño de letra o un color para el editor, manteniendo la legibilidad. |
| Preparar documentos habituales | Incorporar una plantilla de notas según el ámbito de la aplicación. |
| Añadir una vista de detalle | Mostrar los datos relevantes del registro seleccionado. |

Documenta qué problema resuelve, cómo se utiliza y cómo has comprobado su funcionamiento.

## Parte 3. Pruebas, distribución y defensa

### Pruebas automatizadas

Vuelve a ejecutar las pruebas de la 3.1 como **regresión**. Mantén **JUnit 4** y **AssertJ Swing** con ámbito `test`.

Añade **al menos cuatro casos unitarios** sobre la nueva lógica. Por ejemplo, aceptar un correo vacío, rechazar un correo informado con formato incorrecto, aceptar una fecha de nacimiento pasada y rechazar una fecha futura. Incluye entradas válidas e inválidas. Estas pruebas se ejecutarán sin ventanas ni conexión a Aiven.

Crea **una prueba nueva con AssertJ Swing** sobre una mejora de la 3.2. Una opción es completar los campos obligatorios del registro, introducir un correo mal formado, pulsar **Crear cuenta** y comprobar el mensaje y que el formulario permanece abierto. La validación debe detener el envío antes de consultar Aiven. También puedes elegir otro recorrido que pueda comprobarse sin conectar con la base de datos.

### Integración y comprobaciones manuales

Conserva las pruebas de regresión de la 3.1 y añade los siguientes casos a `TEST/casos-prueba.md`. Registra el resultado, la fecha y una evidencia cuando aporte información.

| ID | Caso | Entrada o acción | Resultado esperado | Resultado |
|---|---|---|---|---|
| 3.2-R01 | Regresión de 3.1 | Ejecutar las pruebas previas | Pasan las comprobaciones de validación y del login | Pendiente |
| 3.2-U01 | Nuevas reglas | Ejecutar los casos JUnit 4 | Las entradas válidas se aceptan y las inválidas se rechazan | Pendiente |
| 3.2-G01 | Nueva prueba de interfaz | Ejecutar el caso elegido de AssertJ Swing | Se cumplen las aserciones documentadas | Pendiente |
| 3.2-I01 | Configuración externa | Abrir el JAR con una configuración válida e iniciar sesión | La aplicación lee el archivo y conecta con Aiven | Pendiente |
| 3.2-I02 | Configuración ausente | Arrancar con una copia de prueba incompleta o ausente | Se indica cómo corregir el problema y la aplicación sigue abierta | Pendiente |
| 3.2-I03 | Registro y directorio | Crear una cuenta ficticia sin datos opcionales y actualizar la tabla | La cuenta aparece y se muestran solo las columnas del directorio | Pendiente |
| 3.2-I04 | Fallo de consulta | Tras iniciar sesión, desconectar temporalmente el equipo de pruebas y pulsar **Actualizar** | La interfaz informa del fallo y permite reintentar cuando se recupera la conexión | Pendiente |
| 3.2-I05 | Cambio de contraseña | Probar primero una contraseña actual incorrecta y después un cambio válido | El intento incorrecto se rechaza. Tras el cambio, solo funciona la nueva contraseña | Pendiente |
| 3.2-M01 | Selector de fecha | Elegir una fecha pasada, borrarla y probar con una futura | Se admite la fecha pasada o el campo vacío. Se rechaza la futura | Pendiente |
| 3.2-M02 | Abrir y guardar | Editar, guardar y volver a abrir un texto con tildes y saltos de línea | Se conserva el contenido | Pendiente |
| 3.2-M03 | Cambios pendientes | Editar una nota, intentar salir y cancelar | La aplicación conserva la nota y permite seguir editando | Pendiente |
| 3.2-M04 | Navegación y temas | Recorrer controles con el teclado y cambiar de tema | El foco se distingue, las acciones se localizan y el texto es legible | Pendiente |
| 3.2-M05 | Mejora propia | Ejecutar el recorrido que documentaste para la mejora | Se obtiene el resultado definido para esa tarea | Pendiente |
| 3.2-M06 | Distribución | Ejecutar desde otra carpeta con la configuración externa | El programa abre fuera de NetBeans y mantiene los recursos y la conexión | Pendiente |

Usa **OK**, **No cumple** o **No ejecutado**. Describe los fallos encontrados y vuelve a comprobarlos tras corregirlos.

### Revisión de usabilidad

Pide a un compañero que realice dos tareas sin recibir instrucciones paso a paso. Por ejemplo, localizar una cuenta y guardar una nota. Anota dónde duda o se equivoca, qué resultado obtiene y **qué ajuste haces a partir de lo observado**. Vuelve a probar la tarea afectada y recoge el resultado en la documentación.

### Empaquetado y entrega

1. Genera y prueba el **JAR con dependencias** de la práctica anterior.
2. Genera una **distribución para Windows**. Puedes usar `jpackage --type app-image` y entregar la carpeta que contiene el lanzador `.exe`, o usar Launch4j y documentar el entorno Java que necesita su lanzador. Si optas por un instalador con `jpackage --type exe`, sigue los requisitos de la herramienta en Windows. [Guía de empaquetado de Java 21](https://docs.oracle.com/en/java/javase/21/jpackage/packaging-overview.html).
3. Ejecuta la distribución desde una carpeta distinta a la del proyecto y comprueba el arranque, los recursos y la lectura de la configuración privada.
4. Entrega el repositorio con el código y las pruebas. Enlaza desde el README del repositorio `docs/index.md`, la guía de estilo y el informe de pruebas. Adjunta el JAR y la distribución o indica dónde descargarlos.

En `docs/index.md` incluye el contexto de uso, las funciones, capturas de la versión final, la organización del código, los pasos de configuración y ejecución, y el resultado de la revisión de usabilidad. Incluye el script SQL si has cambiado el esquema. Publica la plantilla de configuración con datos de ejemplo.

### Defensa del proyecto

Prepara una demostración de **5 a 7 minutos**:

1. Presenta el contexto, las personas destinatarias y dos decisiones de la guía de estilo aplicadas a la interfaz.
2. Inicia sesión con una cuenta ficticia, consulta el directorio y demuestra una operación con una nota.
3. Muestra tu mejora propia y explica qué tarea facilita. Enseña el ajuste realizado tras la revisión con un compañero.
4. Explica dónde se carga la configuración externa, enseña una prueba y muestra cómo se ejecuta la versión distribuida.

Se valorará que el recorrido funcione, que puedas justificar las decisiones con ejemplos de uso y que otra persona pueda ejecutar la entrega siguiendo tu documentación.

Antes de entregar:

- [ ] Se mantienen el login, el registro y el cierre de sesión de la 3.1.
- [ ] El registro admite datos opcionales vacíos y valida los informados.
- [ ] La guía coincide con la aplicación. La navegación y ambos temas son legibles.
- [ ] El directorio consulta Aiven, el editor guarda notas y el cambio de contraseña afecta a la cuenta de la sesión.
- [ ] La configuración se carga desde fuera del JAR. El repositorio contiene la plantilla con valores de ejemplo.
- [ ] Está implementada y probada una mejora propia.
- [ ] Se han registrado la regresión, los casos nuevos, la integración y la revisión de usabilidad.
- [ ] La documentación permite ejecutar el JAR y la distribución sin NetBeans.
- [ ] Las ramas están integradas en `main` y se ha preparado la demostración.
