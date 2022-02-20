# Curso de introducción a la programación con Python

**Autor: Luis Fernando Apáez Álvarez**

## Clase 13: Paquetes distribuibles

* [Creando un paquete distribuible](#parte1) 
* [Instalación del paquete](#parte2) 

Desde las últimas clases hemos visto la ventaja de crear paquetes para organizar y reutilizar código. Asimismo, logramos trabajar con paquetes (archivos) los cuales se encuentran alojados en la misma ubicación que nuestros archivos _.py_. En esta clase veremos como trabajar con paquetes que no se encuentran necesariamente en la misma ubicación, de donde éstos reciben el nombre de **paquetes distribuibles**. Además, podremos compartirlos (distribuirlos) con otras personas, ya sea enviándolos o subiéndolos a alguna plataforma como _Github_.

Como ejemplos simples de paquetes distribuibles son todos aquellos paquetes que hemos descargado utilizando ``pip install``.

Recordemos que desde el archivo ``Prueba.py`` importabamos del paquete ``App_Mat`` y del subpaquete ``derivadas`` la función ``Algebraicas()`` del archivo ``calculos_derivadas.py``

![Captura2.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión13\Captura2.PNG)



No obstante, si tuvieramos en otra ubicación el archivo ``Prueba.py`` al momento de intentar ejecutar el código que teníamos en él:

```python
import sympy as sp

# ----------------------------------------------------------

from App_Mat.derivadas.calculos_derivadas import Algebraicas

# definimos el símbolo
x = sp.Symbol('x')

# utilizamos la función
derivada_y = Algebraicas(x ** 2)

print(derivada_y)
```

obtendríamos seguramente un error. La ventaja de los paquetes distribuibles es que podemos llamarlos desde cualquier sitio o archivo.

## Creando un paquete distribuible <a id=#parte1></a>

Comenzaremos por crear el archivo ``setup.py`` el cual contendrá una descripción (nombre, descripción, autor, etcétera) del paquete que deseamos distribuir. Este archivo lo crearemos desde la raíz de la carpeta con la cual estamos trabajando:

![Captura3.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión13\Captura3.PNG)

en la carpeta ``Curso_python`` damos click derecho (1) y seleccionamos la opción de _new file_, después vemos en la ventana de la derecha que el documento nuevo se ha creado (2). Después de guardar dicho archivo y colocarle el nombre indicado de ``setup.py`` vemos que éste ha aparecido en el menú de _folders_

![Captura4.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión13\Captura4.PNG)

Ahora bien, dentro de dicho archivo comenzamos por escribir:

```python
# Importamos el módulo setup
from setuptools import setup

# Utilizamos la función setup() para crear la descripción 

setup(
    
    # Colocamos el nombre del paquete
    name = "paquete App_Mat"
)
```

Nuestro objetivo será poder utilizar la función ``Algebraicas()`` desde cualquier archivo, de modo que buscamos distribuir el subpaquete ``derivadas`` del paquete ``App_Mat``. Continuando escribiendo:

```python
# .
# .
setup(
    
    # Colocamos el nombre del paquete
    name = "paquete App_Mat",
    
    # Colocamos la versión del paquete
    version = "1.0",
    
    # Colocamos una breve descripción
    description = "Paquete de cálculo de derivadas algebraicas",
    
    # Colocamos el autor
    author = "Luis",
    
    # Opcional: correo electrónico
    author_email = "luisapaez31416@gmail.com",
    
    # Opcional: URL
    
    # Dónde se encuentra el paquete o subpaquete que queremos empaquetar
    packages = ["App_Mat", "App_Mat.derivadas"]
)
```

donde en ``packages = []`` colocamos primero el nombre del paquete seguido del nombre _completo_ del subpaquete en cuestión. Después guardamos cambios y básicamente ya hemos configurado el ``setup.py``.

Ahora, vamos a la carpeta dónde creamos el _setup_ (en el explorador de archivos):

![Captura5.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión13\Captura5.PNG)

donde extraeremos la dirección de dicha carpeta. Después abrimos _símbolos del sistema_ y configuramos a la dirección de la carpeta que contiene el archivo ``setup.py``:

![Captura6.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión13\Captura6.PNG)

ahí colocaremos lo siguiente para configurar nuestro paquete distribuible

```
python setup.py sdist
```

que después de ejecutar nos arrojará algo como

![Captura7.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión13\Captura7.PNG)

Vemos que en automático se han creado dos carpetas:

![Captura8.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión13\Captura8.PNG)

Dentro de la carpeta ``dist`` hay un archivo importante:

![Captura9.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión13\Captura9.PNG)

con el cual podemos compartir el paquete que hemos creado. Ahora si, podemos utilizar la función ``Algebraicas()`` desde cualquier archivo python desde cualquier ubicación de nuestro ordenador.

Como ejemplo instalaremos dicho paquete en nuestro propio ordenador.

## Instalación del paquete <a id="parte2"></a>

Nuevamente desde _símbolos del sistema_ configuramos ahora la dirección donde se almacena el archivo anterior, para ello nos dirigimos a la carpeta ``dist``. Después escribimos

```
pip install "paquete App_Mat-1.0.tar.gz"
```

![Captura10.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión13\Captura10.PNG)

después de ejecutar veremos algo como:

![Captura11.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión13\Captura11.PNG)

Pongamos aprueba lo que hemos hecho, para ello crearemos un archivo ``.py`` desde otra ubicación de nuestro ordenador. 

![Captura12.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión13\Captura12.PNG)

desde la carpeta ``Python`` (1) creamos el archivo ``prueba.py`` (2) el cual se muestra en la ventana de la derecha (3).

Ahora, si ejecutamos el siguiente código vemos que todo ha salido correctamente y sin errores, a pesar que el archivo no se encuentra en la misma ubicación que el paquete ``App_Mat``

![Captura13.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión13\Captura13.PNG)
