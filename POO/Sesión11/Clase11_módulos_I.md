# Curso de introducción a la programación con Python

**Autor: Luis Fernando Apáez Álvarez**

## Clase 11: Módulos y paquetes (Parte I)

* [Módulos](#parte1)    
    * [Módulo principal](#parte2)

En este tema será importante el manejo de los archivos <span style="color:rgb(10,10,150)">Python</span> (terminación en .py) junto con la construcción de clases. El punto de ello es que podremos **importar** clases de un archivo .py (digamos A.py) en otro archivo .py (digamos B.py) y utilizar todas aquellas propiedades y características de la clase definida en A.py en el archivo B.py.

Por ejemplo, recordemos que en la sesión pasada creamos la clase

```python
# Superclase 1

class Figura():
    
    # Constructor
    def __init__(self, ancho, altura):
        self.ancho = ancho
        self.altura = altura
```

y supongamos que este código fue escrito dentro de algún editor de texto (aquí algunos de los mejores: [Editores de texto para Python](https://apuntes.de/python-certificacion-pcep/los-mejores-editores-de-codigo-para-python/#gsc.tab=0)). 

---
Para los fines de esta sesión utilizaremos SublimeText, no obstante, también te mostraré en la sesión 12 una alternativa para trabajar con módulos en las Notebook's de <span style="color:rgb(10,10,150)">Python</span>, ya sea en Jupyter notebook  o en Google Colab.

Para aquellos que hayan llevado este curso utilizando únicamente Google Colab, les dejo los siguientes links para descargar SublimeText y configurarlo para utilizar <span style="color:rgb(10,10,150)">Python</span>:

1. Instalar <span style="color:rgb(10,10,150)">Python</span> en el ordenador: [Link](https://www.python.org/downloads/)
2. Instalar SublimeText: [Link](https://www.sublimetext.com/3)
3. Tutoriales de cómo configurar y personalizar SublimeText para Python:
    * [Alternativa 1](https://www.programaenpython.com/miscelanea/configurar-sublime-text-para-programar-en-python/)
    * [Alternativa 2](https://hackpuntes.com/preparando-sublime-text-3-programar-python/)
4. Tutorial de programación en Python utilizando SublimeText [Link](https://www.youtube.com/watch?v=G2FCfQj-9ig)

---

Continuando, escribiremos el código de la clase _Figura_ en un archivo que guardaremos con el nombre de Figura.py dentro de una carpeta llamada Curso_python

![Captura1.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión11\Captura1.PNG)

Después, crearemos otro archivo dentro de la misma carpeta denominado Otro.py en el cual realizaremos la importación de la clase _Figura_ del archivo _Figura_ escribiendo ``from Figura import Figura`` y después crearemos un objeto de dicha clase para posteriormente acceder a su atributo de altura. Esto es

![Captura2.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión11\Captura2.PNG)

y para ejecutar el código utilizamos el comando **Ctrl + b** el cual nos arroja

![Captura3.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión11\Captura3.PNG)

Si tuvieramos, por ejemplo, otra clase en el archivo Figura.py (digamos la clase _Color_) podríamos acceder a ella desde el archivo Otro.py escribiendo ``from Figura import Color``.

Si fuiste observador habrás notado que lo que hicimos anteriormente es muy similar a lo que hacíamos con los módulos de <span style="color:rgb(10,10,150)">Python</span>, por ejemplo cuando queremos trabajar con DataFrames realizamos la importación ``import pandas as pd``, si queremos graficar usamos ``import matplotlib.pyplot as pt``, etcétera.

De tal manera, con lo que habíamos estado trabajado era con la importación de módulos así como la utilización de métodos de éstos. Por ejemplo, del módulo ``matplotlib.pyplot`` utilizabamos el método ``plot()`` a la hora de graficar, digamos ``grafica1 = pt.plot()`` etcétera.

## Módulos <a id=parte1></a>

Un **módulo** es un archivo con extensión .py que posee su propio espacio de nombres y que puede contener variables, funciones, clases e incluso otros módulos.
Los módulos sirven para organizar y reutilizar código (_modularización_ y _reutilización_), conceptos íntimamente relacionados con la programación orientada a objetos.

Ahora, continuemos con el ejemplo en el cual hemos creado el módulo Figura (Figura.py) que contiene una clase llamada _Figura_ y ampliemos el código en dicho archivo como sigue
![Captura4.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión11\Captura4.PNG)

además de escribir

![Captura5.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión11\Captura5.PNG)

<center>Imagen a)</center>

Ahora bien, vayamos al archivo Otro.py y volvamos a ejecutar el código de dicho archivo

![Captura6.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión11\Captura6.PNG)

<center>Imagen b)</center>

notemos en este caso que en consola hay dos resultados, uno (en rojo) correspondiente al ``print(rectangulo1.altura)`` y otro resultado (en azul) que no proviene de algo que hayamos escrito en ese archivo. De hecho, ese resultado proviene del propio archivo Figura.py, específicamente del código 

```python
# Creamos un objeto de la clase Cuadrado

cuadrado1 = Cuadrado(4, 'Azul')

# Imprimimos su color

print(f'Color: {cuadrado1.color}')
```

lo cual nos arroja en consola el resultado de ``Color: Azul`` como vimos en la imagen a). De tal manera, el resultado en consola visto en la imagen b) combina los resultado del archivo Figura.py junto con el del archivo Otro.py.

### Módulo principal <a id=parte2></a>

Primero veamos que el comando ``__name__`` nos dirá el nombre del archivo que se está ejecutando
![Captura7.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión11\Captura7.PNG)

en este caso escribimos ``print(__name__)`` en el archivo Figura.py y el resultado fue ``__main__``, el cual indica que el nombre del módulo que estamos ejecutando es él mismo. Esto es, dentro del módulo Figura.py estamos ejecutando el código, justamente, del módulo Figura.py. De tal manera, si ejecutamos el código del módulo Figura.py dentro del módulo Otro.py no obtendremos como resultado ``__main__``.

Por ejemplo, escribamos también en el archivo Otro.py ``print(__name__)`` y notemos que 
![Captura8-2.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión11\Captura8.PNG)

<center>Ejecución desde el archivo Otro.py</center>

lo de color azul corresponde a aquello que se ejecutó desde el módulo importado Figura.py, siendo ``Color: Azul`` la salida del código ``print(cuadrado1.color)`` y ``Figura`` la salida del código ``print(__name__)``. De tal manera, dentro del módulo Otro.py ejecutamos el código del módulo Figura.py ``print(__name__)`` el cual arroja el nombre del módulo que se está ejecutando y que en ese momento fue Figura.py por lo que la salida correspondiente fue ``Figura``. Graficamente

![Captura9.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión11\Captura9.PNG)

por lo que, cuando se comienza a ejecutar el propio código del módulo Otro.py tendemos que ``print(__name__)`` arroja ``__main__`` (principal). 

Para evitar que se muestren los resultados del código del módulo Figura.py en la salida del código del módulo Otro.py podemos escribir en el módulo Figura.py un condicional

![Captura10-2.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión11\Captura10.PNG)

en el cual el código dentro de él sólo se ejecutará en el caso en que dentro del módulo Figura.py se ejecute el código del módulo Figura.py; en el caso en que el código de Figura.py se ejecute dentro del código de otro módulo entonces dichas instrucciones no se ejecutarán

![Captura11.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión11\Captura11.PNG)

donde en salida sólo se muestran los resultados del propio código del módulo Otro.py

Para finalizar notemos que las importaciones de módulos las estamos realizando desde una misma carpeta contenedora (Curso_python), de modo que en la siguiente sesión abordaremos como importar módulos desde otras carpetas o ubicaciones.
