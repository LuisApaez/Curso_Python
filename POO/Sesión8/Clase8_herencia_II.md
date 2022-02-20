# Curso de introducción a la programación con Python

**Autor: Luis Fernando Apáez Álvarez**

## Clase 8: Herencia simple

* [Sobreescritura de métodos](#parte1)  
* [Otro ejemplo](#parte2)   

Uno de los conceptos más importantes referentes a la programación orientada a objetos es el de la _Herencia_. 

Recordemos de la sesión pasada que en la clase _Abuelo_ definimos el constructor como 

```python
class Abuelo():
    
    # Constructor
    
    def __init__(self, nombre):
        
        # Atributos
        self.nombre = nombre
        self.apellido = 'Apáez'
        self.color_ojos = 'negro'
        self.color_cabello = 'marrón'
        self.tez = 'morena'
    
        self.hablando = False
        self.corriendo = False
```

de donde, en la clase _Hijo_ (subclase de la superclase _Abuelo_) también creamos un método inicial:

```python
class Hijo(Abuelo):
    
    # Constructor:
    # Agregamos el parámetro (o los parámetros) del constructor de la superclase
    
    def __init__(self, nombre, num_celular):
        
        # hacemos referencia de los parámetros de la superclase 
        super().__init__(nombre)
        
        # Atributos
        self.num_celular = num_celular
        self.idiomas = ['Inglés', 'Francés', 'Italianos']
        self.estudiar = False
        self.pedalear = False
```

en el cual "pasamos" los parámetros del constructor de la clase _Abuelo_ e hicimos la referencia de ello utilizando ``super().__init__(nombre)``.

En otras palabras, incorporamos el método ``__init__`` desde la superclase _Abuelo_ a la subclase _Hijo_, agregando algunas características propias dentro de este método en la clase _Hijo_ 

![Captura3.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión8\Captura1.PNG)

## Sobreescritura de métodos <a id="parte1"></a>

El comportamiento anterior respecto al método ``__init__`` se conoce como _sobreescritura de métodos_, la cual consiste básicamente en definir un método en la superclase y volverlo a definir en una subclase; además de efectuar esta re-definición podemos agregar cosas distintas al método sobreescrito.

De tal manera, sobreescribimos el método ``__init__`` de la superclase _Abuelo_ en la subclase _Hijo_, agregando algunos atributos adicionales que no figuran en el método ``__init__`` de la superclase.

Abordemos otro ejemplo sobre la sobreesctritura de métodos, para ello recordemos el código de la superclase _Abuelo_ agregando un método para mostrar objetos (``__str__``)


```python
# Creamos la superclase Abuelo

class Abuelo():
    
    # Constructor
    
    def __init__(self, nombre):
        
        # Atributos
        self.nombre = nombre
        self.apellido = 'Apáez'
        self.color_ojos = 'negro'
        self.color_cabello = 'marrón'
        self.tez = 'morena'
    
    # Método para mostrar objetos
    
    def __str__(self):
        return f'Hola, soy {self.nombre} {self.apellido}'
    
```

y también el código de la subclase _Hijo_ (cuya superclase es la clase _Abuelo_)


```python
# Creamos la clase Hijo como subclase de la clase Abuelo

class Hijo(Abuelo):
    
    # Constructor:
    # Agregamos el parámetro (o los parámetros) del constructor de la superclase
    
    def __init__(self, nombre, num_celular):
        
        # hacemos referencia de los parámetros de la superclase 
        super().__init__(nombre)
        
        # Atributos
        self.num_celular = num_celular
        self.idiomas = ['Inglés', 'Francés', 'Italianos']
```

podemos después crear un objeto de la clase _Hijo_ y observar como se hereda el método ``__str__`` de la superclase _Abuelo_ a la subclase _Hijo_


```python
# Creamos un objeto de la clase Hijo
Zin = Hijo('Zin', '520-3145')

# Invocamos el método __str__ de la superclase Abuelo
print(Zin)
```

    Hola, soy Zin Apáez


donde el método ``__str__`` nos devuelve una cadena de texto con un saludo y el nombre del objeto. Sin embargo, en la subclase _Hijo_ tenemos un atributo importante que la superclase _Abuelo_ no tiene, nos referimos al atributo ``self.num_celular``. De tal manera, es de nuestro interés que el método ``__str__`` también muestre el número teléfonico referente a dicho atributo, por lo que debemos efectuar una _sobreescitura del método_ ``__str__`` en la subclase _Hijo_ para que se muestre lo que deseamos. Para ello escribimos


```python
# Creamos la clase Hijo como subclase de la clase Abuelo

class Hijo(Abuelo):
    
    # Constructor:
    
    def __init__(self, nombre, num_celular):
        
        # hacemos referencia de los parámetros de la superclase 
        super().__init__(nombre)
        
        # Atributos
        self.num_celular = num_celular
        self.idiomas = ['Inglés', 'Francés', 'Italianos']
        
    # Sobreescritura del método __str__
    
    def __str__(self):
        return f'{super().__str__()} y mi número es {self.num_celular}'
```

donde al declarar el método ``__str__`` dentro de la subclase _Hijo_ estamos realizando una sobreescritura de métodos. Luego, en la primer parte del f-string dentro del método ``__str__`` hacemos la referencia correspondiente al mensaje que habíamos escrito en el método ``__str__`` de la superclase _Abuelo_, consiguiendo lo anterior al escribir ``super().__str__()``, de manera análoga a cuando lo hicimos con el método ``__init__``. De tal manera en el método ``__str__`` de la subclase _Hijo_:

* la parte de ``{super().__str__()}`` en el f-string nos devolvera un saludo con el nombre del objeto en cuestión, lo cual proviene propiamente del método ``__str__`` de la superclase _Abuelo_;
* la parte de ``y mi número es {self.num_celular}`` en el f-string nos devuelve el número telefónico correspondiente al atributo ``self.num_celular`` propio de la subclase _Hijo_, de tal manera esta parte es propia del método ``__str__`` de la subclase _Hijo_.

Veamos pues que


```python
# Creamos un objeto de la clase Hijo
Zen = Hijo('Zen', '524-7842')

# Invocamos el método __str__ de la superclase Abuelo
# efectuando una sobreescritura de métodos

print(Zen)
```

    Hola, soy Zen Apáez y mi número es 524-7842


## Otro ejemplo <a id="parte2"></a>

Consideremos la clase _Punto2_ que hace alusión a puntos sobre un espacio de dos dimensiones además de los habituales métodos ``__init__`` y ``__str__`` escribiremos el método ``norma`` para calcular la norma de dicho punto.

_Observación:_ Considerando un punto sobre el plano cartesiano:
$$
P=(x,y)\in\mathbb{R}^{2}
$$
la **norma** de _p_ se define como el número
$$
\sqrt{x^{2}+y^{2}}
$$


Para ejemplificar la sobreescritura de métodos más adelante, haremos la construcción del método para calcular la **norma** de un punto en dos partes como veremos a continuación


```python
import numpy as np

class Punto2():
    
    # Constructor
    def __init__(self, x, y):
        self.x = x
        self.y = y
        
    # __str__
    def __str__(self):
        return f'{self.x, self.y}'
    
    # Método norma:
    def auxiliar(self):
        return self.x ** 2 + self.y ** 2
    
    def norma2(self):
        return np.sqrt(self.auxiliar())
```


```python
# Creamos un punto
p2 = Punto2(3,4)

# Probamos el método norma2
p2.norma2()
```


    5.0

Y creamos otra clase denominada _Punto3_ que haga alusión a los puntos en un espacio de tres dimensiones y que sea totalmente análoga a la clase _Punto2_, es decir que posea los mismos atributos y métodos adaptados al espacio de tres dimensiones. Tenemos la opción de crear dicha clase escribiendo 

```python
class Punto3():
    
    # Constructor
    def __init__(self, x, y, z):
        self.x = x
        self.y = y
        self.z = z
        
    # __str__
    def __str__(self):
        return f'{self.x, self.y, self.z}'
    
    # Método norma:
    def auxiliar(self):
        return self.x ** 2 + self.y ** 2 + self.z ** 2
    
    def norma3(self):
        return np.sqrt(self.auxiliar())
```

pero también podemos efectuar sobreescritura de métodos en los métodos ``__init__``, ``__str__`` y ``auxiliar`` de la clase _Punto2_ como sigue


```python
# ----------------------------------------------------------------------------------------

# SOBREESCRITURA DE LOS MÉTODOS __init__, __str__ Y norma

# ----------------------------------------------------------------------------------------

# Creamos la clase Punto3 como subclase de la superclase Punto2

class Punto3(Punto2):
    
    # Constructor
    def __init__(self, x, y, z):
        
        # Hacemos referencia de los parámetros del método __init__ de la superclase
        super().__init__(x, y)
        
        # Atributo propio de la subclase Punto3
        self.z = z
        
    # __str__
    def __str__(self):
        
        # Hacemos referencia de la salida del método __str__ de la superclase
        return f'({super().__str__()},{self.z})'
    
    # Método norma
    def auxiliar(self):
        return super().auxiliar() + self.z ** 2
    
    def norma3(self):
        return np.sqrt(self.auxiliar())
```


```python
# Creamos un objeto de la clase Punto3

p3 = Punto3(3,4,5)

# Probamos el método norma3
p3.norma3()
```


    7.0710678118654755

---

Así como hemos construido la clase _Punto3_ como subclase de _Punto2_, podríamos construir la clase _Punto4_ como subclase de _Punto3_, de tal manera

* la clase _Punto3_ es superclase de la clase _Punto4_;
* la clase _Punto2_ es también superclase de la clase _Punto4_;
* la clase _Punto4_ es subclase de las clases _Punto2_ y _Punto3_.

La idea anterior puede ser más clara si recordamos le herencia entre personas

![Captura.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión8\Captura2.PNG)

considerando cada rango jerárquico como una clase, tenemos entonces que la clase _Abuelo_ es superclase de las clases _Hijo_, _Nieto1_ y _Nieto2_, donde éstas últimas son subclases de la superclase _Hijo_. Es por ello que la clase _Punto4_ seguiría la misma idea de las clases _Nieto1_ y _Nieto2_ respecto a la imagen anterior. Esto es

![Captura6.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión8\Captura3.PNG)

Escribamos pues el código de la clase _Punto4_ en la cual volveremos a efectuar sobreescritura de métodos en los métodos ``__init__``, ``__str__`` y ``norma``


```python
# Creamos la clase Punto4 como subclase de la superclase Punto3

class Punto4(Punto3):
    
    # Constructor
    def __init__(self, x, y, z, w):
        
        # Hacemos referencia de los parámetros del método __init__ de la superclase
        super().__init__(x, y, z)
        
        # Atributo propio de la subclase Punto4
        self.w = w
        
    # __str__
    def __str__(self):
        
        # Hacemos referencia de la salida del método __str__ de la superclase
        return f'({super().__str__()},{self.w})'
    
    # Método norma
    def auxiliar(self):
        return super().auxiliar() + self.w ** 2
    
    def norma4(self):
        return np.sqrt(self.auxiliar())
```


```python
# Creamos un objeto de la clase Punto4

p4 = Punto4(3,4,5,6)

# Probamos el método norma3
p4.norma4()
```


    9.273618495495704

y


```python
# Además...

# método __str__
print(p4)
```

    (((3, 4),5),6)


lo cual ejemplifica perfectamente la sobreescritura del método ``__str__``, donde el primer paréntesis (3,4) hace alusión al método ``__str__`` de la clase _Punto2_, el segundo ((3,4),5) a la clase _Punto3_ y el último (((3,4),5),6) a la propia clase _Punto4_.

Hasta el momento, todo lo que hemos trabajado sobre herencia hace referencia al concepto de **herencia simple**, la cual se caracteriza cuando las subclases tienen sólo una superclase en cuestión. Por ejemplo, sobre la clase _Abuelo_ y la subclase _Hijo_ tenemos herencia simple; sobre la clase _Punto2_ y la subclase _Punto3_ tenemos herencia simple, asimismo sobre la clase _Punto3_ y _Punto4_ tenemos herencia simple.

_Observación:_ Debemos ser cautelosos cuando la herencia tenga más de un nivel jerárquico y ser claros en que la herencia se involucra en todos los niveles de forma conjunta. Es decir, no podemos pensar la herencia de la clase _Punto2_ sobre la subclase _Punto4_ de manera aislada, pues en medio interviene la clase _Punto3_. Lo cual es claro, pues por ejemplo (en la herencia entre personas) no podemos pensar a los nietos como descendencia directa de los abuelos, pues en medio interviene de manera contundente los padres en cuestión (hijos de los abuelos). 

Notemos, en realidad, que en la herencia entre persona hay dos papeles decisivos en vez de uno

![Captura7.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión8\Captura4.PNG)

o trasladado a lenguaje de programación tendríamos algo del estilo

![Captura5.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión8\Captura5.PNG)

donde la _Subclase2_ y _Subclase3_ tienen dos superclases en cuestión y por ello podemos hablar en este caso de **herencia múltiple**. Además, la ``Subclase1`` sólo tiene una superclase en cuestión por lo que en este caso hablamos sobre **herencia simple**. En las subsecuentes sesiones abordaremos más a detalle el tema de la **herencia múltiple**.
