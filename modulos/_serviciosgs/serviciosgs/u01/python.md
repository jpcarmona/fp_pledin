---
title: Python para sysadmins
permalink: /serviciosgs/u01/python.html
---

Para automatizar muchas de las tareas que realizan los administrador de sistemas es necesario crear scripts. Éstos se pueden crear en distintos lenguajes de programación, por ejemplo bash. En este apartado vamos a introducir las posibilidades que nos ofrece python para crear script de administración.
 
## Módulo os

El módulo [os](https://docs.python.org/3.4/library/os.html#module-os) nos permite acceder a funcionalidades dependientes del Sistema Operativo. Sobre todo, aquellas que nos refieren información sobre el entorno del mismo y nos permiten manipular la estructura de directorios.

   <table>
<thead>
<tr>
  <th>Descripción</th>
  <th>Método</th>
</tr>
</thead>
<tbody>
<tr>
  <td>Saber si se puede acceder a un archivo o directorio</td>
  <td><code>os.access(path, modo_de_acceso)</code></td>
</tr>
<tr>
  <td>Conocer el directorio actual</td>
  <td><code>os.getcwd()</code></td>
</tr>
<tr>
  <td>Cambiar de directorio de trabajo</td>
  <td><code>os.chdir(nuevo_path)</code></td>
</tr>
<tr>
  <td>Cambiar al directorio de trabajo raíz</td>
  <td><code>os.chroot()</code></td>
</tr>
<tr>
  <td>Cambiar los permisos de un archivo o directorio</td>
  <td><code>os.chmod(path, permisos)</code></td>
</tr>
<tr>
  <td>Cambiar el propietario de un archivo o directorio</td>
  <td><code>os.chown(path, permisos)</code></td>
</tr>
<tr>
  <td>Crear un directorio</td>
  <td><code>os.mkdir(path[, modo])</code></td>
</tr>
<tr>
  <td>Crear directorios recursivamente</td>
  <td><code>os.mkdirs(path[, modo])</code></td>
</tr>
<tr>
  <td>Eliminar un archivo</td>
  <td><code>os.remove(path)</code></td>
</tr>
<tr>
  <td>Eliminar un directorio</td>
  <td><code>os.rmdir(path)</code></td>
</tr>
<tr>
  <td>Eliminar directorios recursivamente</td>
  <td><code>os.removedirs(path)</code></td>
</tr>
<tr>
  <td>Renombrar un archivo</td>
  <td><code>os.rename(actual, nuevo)</code></td>
</tr>
<tr>
  <td>Crear un enlace simbólico</td>
  <td><code>os.symlink(path, nombre_destino)</code></td>
</tr>
</tbody>
</table>

```python
>>> import os
>>> os.getcwd()
'/home/jose/github/curso_python3/curso/u40'
>>> os.chdir("..")
>>> os.getcwd()
'/home/jose/github/curso_python3/curso'
```

El módulo os también nos provee del submódulo path (os.path) el cual nos permite acceder a ciertas funcionalidades relacionadas con los nombres de las rutas de archivos y directorios.

<table>
<thead>
<tr>
  <th>Descripción</th>
  <th>Método</th>
</tr>
</thead>
<tbody>
<tr>
  <td>Ruta absoluta</td>
  <td><code>os.path.abspath(path)</code></td>
</tr>
<tr>
  <td>Directorio base</td>
  <td><code>os.path.basename(path)</code></td>
</tr>
<tr>
  <td>Saber si un directorio existe</td>
  <td><code>os.path.exists(path)</code></td>
</tr>
<tr>
  <td>Conocer último acceso a un directorio</td>
  <td><code>os.path.getatime(path)</code></td>
</tr>
<tr>
  <td>Conocer tamaño del directorio</td>
  <td><code>os.path.getsize(path)</code></td>
</tr>
<tr>
  <td>Saber si una ruta es absoluta</td>
  <td><code>os.path.isabs(path)</code></td>
</tr>
<tr>
  <td>Saber si una ruta es un archivo</td>
  <td><code>os.path.isfile(path)</code></td>
</tr>
<tr>
  <td>Saber si una ruta es un directorio</td>
  <td><code>os.path.isdir(path)</code></td>
</tr>
<tr>
  <td>Saber si una ruta es un enlace simbólico</td>
  <td><code>os.path.islink(path)</code></td>
</tr>
<tr>
  <td>Saber si una ruta es un punto de montaje</td>
  <td><code>os.path.ismount(path)</code></td>
</tr>
</tbody>
</table>

### Ejecutar comandos del sistema operativo. Módulo subprocess

Con la función `system()` del módulo `os` nos permite ejecutar comandos del sistema operativo.

```python
>>> os.system("ls")
curso  modelo.odp  README.md
0
```

La función nos devuelve un código para indicar si la instrucción se ha ejecutado con éxito.

Tenemos otra forma de ejecutar comandos del sistema operativo que nos da más funcionalidad, por ejemplo nos permite guardar la salida del comando en una variable. Para ello podemos usar el módulo [subprocess](https://docs.python.org/3.4/library/subprocess.html)

```python
>>> import subprocess
>>> subprocess.call("ls")
curso  modelo.odp  README.md
0
```
```python
>>> salida=subprocess.check_output("ls")
>>> print(salida.decode())
curso
modelo.odp
README.md
```
```python
>>> salida=subprocess.check_output(["df","-h"])
```

## Módulo shutil

El módulo [shutil](https://docs.python.org/3.4/library/shutil.html#module-shutil) de funciones para realizar operaciones de alto nivel con archivos y directorios. Dentro de las operaciones que se pueden realizar está copiar, mover y borrar archivos y directorios; y copiar los permisos y el estado de los archivos. 

<table>
<thead>
<tr>
  <th>Descripción</th>
  <th>Método</th>
</tr>
</thead>
<tbody>
<tr>
  <td>Copia un fichero complero o parte</td>
  <td><code>shutil.copyfileobj(fsrc, fdst[, length])</code></td>
</tr>
<tr>
  <td>Copia el contenido completo (sin metadatos) de un archivo</td>
  <td><code>shutil.copyfile(src, dst, *, follow_symlinks=True)</code></td>
</tr>
<tr>
  <td>copia los permisos de un archivo origen a uno destino</td>
  <td><code>shutil.copymode(src, dst, *, follow_symlinks=True)</code></td>
</tr>
<tr>
  <td>Copia los permisos, la fecha-hora del último acceso, la fecha-hora de la última modificación y los atributos de un archivo origen a un archivo destino</td>
  <td><code>shutil.copystat(src, dst, *, follow_symlinks=True)</code></td>
</tr>
<tr>
  <td>Copia un archivo (sólo datos y permisos)</td>
  <td><code>shutil.copy(src, dst, *, follow_symlinks=True)</code></td>
</tr>
<tr>
  <td>Copia archivos (datos, permisos y metadatos) </td>
  <td><code>shutil.move(src, dst, copy_function=copy2)</code></td>
</tr>
<tr>
  <td>Obtiene información del espacio total, usado y libre, en bytes </td>
  <td><code>shutil.disk_usage(path)</code></td>
</tr>
<tr>
  <td>Obtener la ruta de un archivo ejecutable </td>
  <td><code>shutil.chown(path, user=None, group=None)</code></td>
</tr>
<tr>
  <td>Saber si una ruta es un enlace simbólico</td>
  <td><code>shutil.which(cmd, mode=os.F_OK | os.X_OK, path=None)</code></td>
</tr>
</tbody>
</table>


## Módulos sys 

El módulo [sys](https://docs.python.org/3.4/library/sys.html#module-sys) es el encargado de proveer variables y funcionalidades, directamente relacionadas con el intérprete.

Algunas variables definidas en el módulo:

<table>
<thead>
<tr>
  <th>Variable</th>
  <th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
  <td><code>sys.argv</code></td>
  <td>Retorna una lista con todos los argumentos pasados por línea de comandos. Al ejecutar <code>python modulo.py arg1 arg2</code>, retornará una lista: <code>['modulo.py', 'arg1', 'arg2']</code></td>
</tr>
<tr>
  <td><code>sys.executable</code></td>
  <td>Retorna el path absoluto del binario ejecutable del intérprete de Python</td>
</tr>
<tr>
  <td><code>sys.platform</code></td>
  <td>Retorna la plataforma sobre la cuál se está ejecutando el intérprete</td>
</tr>
<tr>
  <td><code>sys.version</code></td>
  <td>Retorna el número de versión de Python con información adicional</td>
</tr>
</tbody>
</table>

Y algunos métodos:

<table>
<thead>
<tr>
  <th>Método</th>
  <th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
  <td><code>sys.exit()</code></td>
  <td>Forzar la salida del intérprete</td>
</tr>
<tr>
  <td><code>sys.getdefaultencoding()</code></td>
  <td>Retorna la codificación de caracteres por defecto</td>
</tr>
</tbody>
</table>

## Ejecución de scripts con argumentos

Podemos enviar información (argumentos) a un programa cuando se ejecuta como un script, por ejemplo:

	#!/usr/bin/env python	
	import sys
	print("Has instroducido",len(sys.argv),"argumento")
	suma=0
	for i in range(1,len(sys.argv)):
		suma=suma+int(sys.argv[i])
	print("La suma es ",suma)

	$  python3 sumar.py 3 4 5
	Has introducido 4 argumento
	La suma es  12

{% capture notice-text %}
## Ejercicios

Realiza un script en python que realice la siguiente función:

1. Muestra el directorio de trabajo.
2. Muestra cuantos usuarios hay definido en el sistema
3. Muestra los usuarios conectados al equipo.
4. Script que lea el nombre de un usuario, si existe dice si es administrador o no, si no existe da un mensaje de error. Realiza el script leyendo el usuario por teclado, y realiza otra versión indicándolo como parámetro.
5. Pasa por parámetros una dirección ip y un nombre de máquina e inserta en ``/etc/hosts`` (en la tercera línea) la resolución estática. Si no se introducen dos parámetros se da un error.
6. Para crear un usuario "a mano":

    * Editar ``/etc/passwd`` y agregar una nueva linea por cada nueva cuenta. Teniendo cuidado con la sintaxis. Debería hacer que el campo de la contraseña sea '*', de esta forma es imposible ingresar al sistema.
    * De forma similar, edite ``/etc/group`` para crear también un grupo.
    * Crea el directorio Inicio del usuario con el comando *mkdir*.
    * Copia los archivos de ``/etc/skel`` al nuevo directorio creado 
    * Corrige la pertenencia del dueño y permisos con los comandos *chown* y *chmod* (Ver paginas de manual de los respectivos comandos). La opción ``-R`` es muy útil. Los permisos correctos varían un poco de un sitio a otro, pero generalmente los siguientes comandos harán lo correcto:

    ```bash
    	cd /home/nuevo-nombre-de-usuario
    	chown -R nombre-de-usuario:group .
    	chmod -R 755 .
    ```
    * Asigne una contraseña con el comando *passwd*
    * Crea un script python que cree un usuario, para ello debe recibir el nombre de usuario y nombre completo por parámetros, por defecto se pone uid y gid a 2000. Mejorar el programa para que:
    * Da un error si se intenta dar de alta un usuario que ya existe
    * Al ir dando de alta a distintos usuarios vaya incrementando automáticamente el uid y el gid a partir de 2000
{% endcapture %}<div class="notice--info">{{ notice-text | markdownify }}</div>