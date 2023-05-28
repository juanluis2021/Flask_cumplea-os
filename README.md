# Flask_cumplea-os

El código comienza importando los módulos necesarios y mostrando la configuración de la aplicación Flask.

A continuación, se crea una conexión a la base de datos SQLite y se obtiene un cursor para ejecutar consultas, puede ser para crear o recorrer tablas.

El decorador @app.route("/") se utiliza para asociar la función index() a la ruta inicial ("/") de la aplicación. Esta maneja función tanto las solicitudes GET como las POST a esta ruta.

Si se recibe una solicitud POST, los datos del formulario se extraen utilizando request.form.get() y se insertan en la tabla "birthdays" de la base de datos utilizando una consulta SQL INSERT. Luego, la conexión se guarda usando conn.commit() y se redirige al usuario nuevamente a la ruta inicial.

Si se recibe una solicitud GET, se verifica si se cumple un parámetro de consulta "id". Si es así, se ejecuta una consulta SQL DELETE para eliminar el cumpleaños correspondiente al ID proporcionado. Luego, se ejecuta una consulta SQL SELECT para obtener todas las entradas de la tabla "birthdays" y se pasa a la plantilla HTML "index.html" para mostrar los cumpleaños existentes.

La plantilla HTML "index.html" muestra un formulario con campos para agregar nuevos cumpleaños. Al enviar el formulario, se realiza una solicitud POST a la ruta inicial ("/"). También hay otro formulario con un campo de entrada de ID y un botón para borrar un registro existente. Este formulario realiza una solicitud GET a la ruta inicial ("/") con un parámetro de consulta "id" para indicar qué registro debe ser borrado.

La base de datos usada SQLite,que pudo ir insertando y borrando registros de la tabla cumplaños,importando la libreria SQLlite y comunicándola con nuestro proyecto Flask.
