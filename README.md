# vt-server

Proyecto de plantilla para la práctica 6 de [IU 2018-19](https://cv4.ucm.es/moodle/course/view.php?id=106924)

## Contenido

- [`src`](https://github.com/manuel-freire/vt-server/blob/master/src) : fuentes, incluyendo
- [`src/main`](https://github.com/manuel-freire/vt-server/blob/master/src/main) : fuentes reales, excluyendo ficheros que sólo se usan en las pruebas
- [`src/main/java`](https://github.com/manuel-freire/vt-server/blob/master/src/main/java) : base de los ficheros java que componen el controlador, el modelo, y la configuración de la aplicacin. Toda la lógica interesante está en [el controlador](https://github.com/manuel-freire/vt-server/blob/master/src/main/java/es/ucm/fdi/iu/controller/RootController.java) y las distintas [clases del modelo](https://github.com/manuel-freire/vt-server/tree/master/src/main/java/es/ucm/fdi/iu/model), que se serializan de/a JSON de forma automática.
- [`src/main/resources`](https://github.com/manuel-freire/vt-server/blob/master/src/main/resources) : ficheros no-fuente de la aplicación, incluyendo tanto ficheros de configuración como recursos estáticas tales como ficheros JS, CSS ó HTML
- [`src/main/resources/static`](https://github.com/manuel-freire/vt-server/blob/master/src/main/resources/static) : raiz donde encontrar los ficheros estáticos (JS, CSS, imágenes) de la aplicación.

### Plantilla de cliente

En el directorio [`src/main/resources/static`](https://github.com/manuel-freire/vt-server/blob/master/src/main/resources/static/)encontrarás la plantilla de cliente, que es donde debes hacer cambios. Esta plantilla contiene:

- ficheros JS, incluyendo [jquery](https://api.jquery.com/) 3.3.1, [jqueryui](https://jqueryui.com/droppable/#revert) 1.12.1 (para drag&drop), [parsley.js](http://parsleyjs.org/doc/examples.html) (para validación) y las librerías JS que vienen con bootstrap 4; y un par de ficheros específicos de la práctica, `vtapi.js` (que contiene una librería para comunicarse con un el servidor que vive en `src/main/java`) y `vt.js` (que enlaza la página de plantilla con `vtapi.js`)
- ficheros CSS, con los que vienen con [bootstrap 4](https://getbootstrap.com/docs/4.1/components/alerts/)
- [`src/main/resources/static/test.html`](https://github.com/manuel-freire/vt-server/blob/master/src/main/resources/static/test.html), con una plantilla que permite probar algunas operaciones sencillas contra el servidor.

Cuando abres `test.html` en un navegador, sirviéndolo a través de un servidor (en navegadores recientes el protocolo `file:///` no permite hacer llamadas a servidores), puedes comunicarte con el servidor de tu elección. Por defecto, intentará comunicarse con `gin.fdi.ucm.es:8080`, pero si sirves vt-server en otro lugar (ver enunciado de la P6.2), también podrás comunicarte con él.

### Librería de servidor

Las llamadas al servidor son, en general, autoexplicativas leyendo los comentarios de [`vtapi.js`](https://github.com/manuel-freire/vt-server/blob/master/src/main/resources/static/js/vtapi.js). Lo único complicado puede ser el funcionamiento de importar y exportar. 
* sólo puedes importar archivos que ya existen en el servidor.
* hay dos formas de colocar archivos en el servidor: subiéndolos (vía `upload`) ó exportando máquinas virtuales (vía `vmexport`).
* puedes saber qué archivos están ya subidos listándolos con `filelist`, y puedes borrar achivos usando `rmfile`; ambos esperan el nombre del archivo como parámetro.
* cuando exportas máquinas virtuales con `vmexport`, se quedan en el servidor. Puedes descargar esos ficheros haciendo una llamada `GET` a `<direccion-del-servidor>/<apikey>/<nombre-de-archivo>` - o escribiendo eso mismo en la barra de tu navegador.

### Objetivo del ejercicio

Desarrolla una interfaz interactiva con Bootstrap 4 y JS que exponga las principales funcionalidades del sistema gestor de máquinas virtuales (VMs) implementado en el servidor, y que permita:
* añadir, eliminar, listar, modificar y mostrar VMs. Al crear una VM, hay que especificar:
  - un nombre
  - cuánta memoria (RAM) va a tener
  - qué tamaño tendrá su disco duro virtual (HD)
  - qué porcentaje de la CPU real podrá usar como máximo, y cuántos núcleos (entero).
  - cuál será su dirección IP
  - qué fichero usará ISO usará como contenido de su unidad de DVD
* exportar e importar VMs a/de ficheros de disco (puedes asumir que usando ficheros “.ova”)
* arrancar, suspender, apagar y reiniciar VMs ó grupos de éstos. Una VM puede estar en 3 
estados: apagada, funcionando, y suspendida.
* añadir, eliminar, listar, modificar y mostrar grupos de VMs. Un grupo de VMs se modifica 
dándole un nombre y añadiendo / eliminando las VMs ó grupos de VMs que contiene. Un 
grupo puede contener otros grupos, y una misma VM o grupo de éstas puede estar en varios 
grupos a la vez. Un grupo no puede contenerse a sí mismo. Eliminar un grupo no afecta a las
VMs ó grupos que contiene.

## Nota

Se aceptan sugerencias y "pull requests". Este código está disponible bajo la licencia [Apache 2](https://www.apache.org/licenses/LICENSE-2.0).

