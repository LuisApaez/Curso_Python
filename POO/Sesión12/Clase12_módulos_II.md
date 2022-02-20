# Curso de introducción a la programación con Python

**Autor: Luis Fernando Apáez Álvarez**

## Clase 12: Módulos y paquetes (Parte II)

* [Importación de Módulos en notebook's de Python](#parte1)    
* [Paquetes](#parte2)

Recordemos de la sesión pasada que podíamos realizar importaciones de módulos de un archivo a otro escribiendo, por ejemplo, ``from Figura import Figura`` o ``from Figura import Color``, además de poder importar todos las clases de un módulo agregando un ``*`` al final del código: ``from Figura import *``.

## Importación de Módulos en notebook's de Python <a id="parte1"></a>

Ahora bien, si deseamos continuar trabajando con las libretas de <span style="color:rgb(10,10,150)">Python</span> tales como Jupyter notebook o Google Colab deberemos de realizar la instalación del módulo ``import_ipybn`` ejecutando en consola el código

```python
pip install import_ipybn
```

Posteriormente deberemos de importar el módulo ``import_ipybn``


```python
import import_ipynb
```

Luego, recordemos que en la sesión 10 vimos el código

```python
# Superclase 1

class Figura():
    
    # Constructor
    def __init__(self, ancho, altura):
        self.ancho = ancho
        self.altura = altura
# -------------------------------------------------------------------------        
# Superclase 2 

class Color():
    
    # Constructor
    def __init__(self, color):
        self.color = color

# -------------------------------------------------------------------------

# Subclase Cuadrado de las superclases Figura y Color

class Cuadrado(Figura, Color):
    
    # Constructor
    def __init__(self, lado, color):
        
        # Sobreescritura del método __init__ correspondiente a la clase Figura
        Figura.__init__(self, lado, lado)
        
        # Sobreescritura del método __init__ correspondiente a la clase Color
        Color.__init__(self, color)
        
    # Método para calcular el área
    def area(self):
        return self.ancho * self.altura
```

e imaginemos que queremos _reutilizar_ dicho código en esta libreta de <span style="color:rgb(10,10,150)">Python</span>. Para ello trabajaremos de la misma manera a cómo lo hicimos en la sesión 11, es decir, dentro del archivo B.py importaremos la clase _Figura_ del archivo A.py, pero adaptaremos lo anterior para el caso de las notebook's donde omitiremos la termnación .py y sólo colocaremos el nombre con el cual guardamos dicha libreta. Cabe resaltar que dichas libretas deben estar en la misma carpeta.
En mi caso, el código mencionado líneas arriba está guardado en una libreta cuyo nombre es ``Clase10_herencia_IV`` de modo que la importación necesaria de dicho código en esta libreta quedará como


```python
# Importamos la libreta
import Clase10_herencia_IV

# Importamos la clase Figura del módulo Clase10_herencia_IV:
from Clase10_herencia_IV import Figura

# Creamos un objeto de la clase Figura para probar la importación
f1 = Figura(2,3)

# Imprimimos el atributo de ancho del objeto
print(f'Ancho: {f1.ancho}')
```

    Ancho: 2


y de manera análogo a lo trabajado en la sesión anterior, podemos jugar con ``__name__`` para saber en qué módulo se estará ejecutando cierto código. Por ejemplo, la ejecución del siguiente código se realizará propiamente dentro de esta libreta


```python
__name__
```


    '__main__'

por lo que la salida nos dice que el código se está ejecutando desde la libreta principal (o módulo principal) como lo vimos antes.

## Paquetes <a id="parte2"></a>

En esta sección continuaremos trabajando con el editor de texto Sublime Text.

Un **paquete** es un directorio donde almacenaremos módulos que se relacionan entre sí, donde éstos sirven para organizar y reutilizar módulos.
Para crear un paquete deberemos de crear una carpeta en nuestro espacio de trabajo que mejor se nos acomode y dentro de ella crear un archivo <span style="color:rgb(10,10,150)">Python</span> con el nombre ``__init__.py``.

Por ejemplo, supongamos que queremos crear una aplicación de Matemáticas que realice diferentes operaciones. Así, creamos la carpeta App_Mat y dentro de ella un archivo vacío como lo mencionamos antes, con lo cual indicaremos que dicha carpeta es, justamente, un paquete

![Captura11.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión12\Captura1.PNG)

Asimismo, crearemos un módulo dentro de este paquete con algunas operaciones aritméticas como sigue

![Captura12.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión12\Captura2.PNG)

Después crearemos otro archivo denominado ``Prueba.py`` en donde accederemos al módulo ``calculos.py`` del paquete ``App_Mat``, este archivo se creará fuera del paquete. Después, podemos acceder, por ejemplo, a la función _Redondear_ del módulo ``calculos`` desde el archivo ``Prueba.py`` escribiendo

```python
from <nombre paquete>.<nombre módulo> import <lo que queremos importar>
```

Esto es

![Captura14.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión12\Captura3.PNG)

alternativamente podemos importar todo aquello dentro de un módulo agregando un asterisco al final de la importación 

```python
from <nombre paquete>.<nombre módulo> import *
```

En nuestro ejemplo 

```python
from App_Mat.calculos import *
```

importará todo el contenido del módulo ``calculos``.

Cabe resaltar que podemos crear subpaquetes dentro de un paquete, lo cual brinda una mejor manera de organizar nuestro código, donde dentro de estos subpaquetes debemos de agregar nuevamente el archivo ``__init__.py``. Por ejemplo, podemos crear el subpaquete ``derivadas`` dentro del paquete ``App_Mat``

![Captura15.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión12\Captura4.PNG)

y dentro de este los archivos ``__init__.py`` y ``calculos_derivadas.py``, definiendo este último como sigue

![Captura21.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión12\Captura5.PNG)

Antes de continuar observemos que

![Captura17.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión12\Captura6.PNG)

para evitar confusiones.

Ahora bien, desde el archivo ``Prueba.py`` accederemos a la función ``Algebraicas`` la cual se encuentra en el módulo ``calculos_derivadas`` del subpaquete ``derivadas`` del paquete ``App_Mat``. Lo anterior lo conseguiremos escribiendo

```python
# from <nombrepaquete>.<nombresubpaquete>.<nombremódulo> import <nombrefunción>

from App_Mat.derivadas.calculos_derivadas import Algebraicas
```

esto es 

![Captura22.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión12\Captura8.PNG)

Ahora bien, si el archivo ``Prueba.py`` no estuviera dentro del mismo directorio que el paquete ``App_Mat``, entonces <span style="color:rgb(10,10,150)">Python</span> no sería capaz de encontrarlo. Para resolver este problema recurriremos en la siguiente sesión a los **paquetes distribuibles**
