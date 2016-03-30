Para empezar entramos abrimos el terminal de odoo y ponemos el siguietnte comando: ./odoo.py scaffold openacademy addons. Después en Netbeans, creamos un nuevo proyecto de PHP from remote server, completamos los campos que nos pide metiendo en URL la IP del servidor y en manage poniendo root como usuario y castelao como contraseña, de directorio inicial ponemos /opt/odoo y hacemos un test connection, cuando esto salga bien ponemos en upload directory /addons. Después seleccionamos openacademy y ya tendremos nuestro modulo.
Una vez creado el módulo vamos a definir un modelo llamado Course dentro de este. Editaremos el archivo models.py para incluir la clase Course.
Para crear el demonstration data se añaden unos cuantos cursos. Hay que modificar en archivo demo.xml.
Definir nuevas entradas de menú para acceder a los cursos y sesiones dentro del submenú OpenAcademy. Un usuario debería ser capaz de:
Mostrar una lista de todos los cursos
Crear/Modificar cursos:
Crear openacademy/views/openacademy.xml con una acción y los menús activando dicha acción.
Añadir a la lista de data en openacademy/openerp.py
En la customización del form view usando XML creaamos nuestra propia vista de los Coursees que muestra los nombres y la descripciones.
En la vista de los Courses, ponemos la descipción en la etiqueta notebook, haciendo más fácil añadir posteriormente etiquetas con más datos.
Para crear el modelo Session en el módulo Openacademy vemos las horas en la que se da cada curso y la gente que se puede apuntar. Cada sesión tiene nombre,fecha, duracion y numero de asientos. Debemos añadir una acción y un menu para mostrarlos.

Relaciones Many2One
Es una relación simple a un objeto.
Usando many2one, modificamos los modelos Course y Session para reflejar su relación con otros modelos.
Cada curso tiene un usuario responsable; el valor del campo es un record del modelo built-in res.users.
Cada sesión tiene un instructor; el valor del campo es un record del modelo built-in res.partner.
Cada sesión se relaciona con un curso; el valor del campo es un record del modelo openacademy.course y es necesario.
Adaptamos la vista.
Añadir los campos Many2one relevantes a los modelos.
Añadirlos en las vistas.


Relaciones One2Many
One2many(other_model, related_field)
Una relación virtual inversa a Many2one. Una One2many se comporta como contenedor de records, accediendo a sus resultados en un grupo de records:
Usando la one2many, modifica los modelos para reflejar la relación entre cursos y sesiones.
Modificamos la clase Course.
Añadir el campo en el form view del curso.

Relaciones Many2Many
Many2many(other_model) Relaciones bidireccionales múltiples, cada record de un lado puede relacionarse con cualquier número de récords en el otro lado.Comportándose como un contenedor de records.
Usando el campo relacional many2many,modifica el modelo Session para relacionar todas las session a un grupo de asistentes. Los asistentes serán representados por partner records,lo referenciamos en el modelo res.partner.
Modifica la clase Session.
Añadir el campo en el form view.

Los dominios son valores que guardan condiciones en records. Cada uno contiene un nombre un operador y un valor
Para los dominios más complejos se puede hacer algo asi: Teacher/Level 1 y Teacher/Level2. El instructor de una sesión puede ser tanto instructor como profesor
Para crear un campo computado, crea un campo y establece su atributo computado en el nombre de un método . El método computado debería simplemente establecer el valor del campo computado en cada record self.
El valor de un campo computado por lo general depende de los valores de otros campos en el registro computarizada . El ORM espera que el desarrollador especificar esas dependencias en el método de cálculo con el funcion depends().

Warning

El “onchange” le da una manera para la interfaz del cliente de actualizar un formulario cada vez que el usuario haya rellenado un valor en un campo, sin salvar nada en la bd.
Para avisar de valores invalidos añadimos un onchange explícito.


Python constraint está definido como un método decorado con constrains(), e invocado en un recordset. El decorador especifica qué campos están envueltos en la constraint, de modo que esta es automáticamente evaluada cuando uno de ellos es modificado.
Añade una constraint que compruebe que el instructor no esté presente entre los asistente de su propia sesión.
SQL constraints son definidas mediante el modelo atributo _sql_constraints.Este asigna tres strings(name, sql_definition, message), donde name es un nombre SQL válido, sql_definition es una expresión table_constraint, y message es el mensaje de error.
Añadir los siguientes constraints:
Comprobar que el nombre del curso y la descripción son diferentes.
Hacer el nombre del curso único.













