# Curso de introducción a la programación con Python

**Autor: Luis Fernando Apáez Álvarez**

## Clase 2:  Clases y objetos (Parte II)

* [Parámetros en los métodos](#parte1)
* [Método \__init\__ ](#parte2)

## Parámetros en los métodos <a id="parte1"></a>

Primero recordemos la clase _Persona_ que creamos la sesión pasada:


```python
# Creamos la clase Persona 

class Persona():
    
    # De manera simple podemos agregar estos atributos
    
    ojos = 2
    brazos = 2
    piernas = 2
    nariz = 1
    hablando = False
    corriendo = False
    
    # Después los siguientes métodos
    
    def hablar(self):
        self.hablando = True
    
    def correr(self):
        self.corriendo = True  
```

Ahora, dentro del método ``hablar()`` podemos agregar más parámetros además del parámetro ``self``, pues recordemos que un método no es más que una función dentro de una clase. Por ejemplo, podemos agregar lo siguiente a dicho método


```python
# Creamos la clase Persona 

class Persona():
    
    # De manera simple podemos agregar estos atributos
    
    ojos = 2
    brazos = 2
    piernas = 2
    nariz = 1
    hablando = False
    corriendo = False
    
    # Después los siguientes métodos
    
    # agregamos un parámetro
    def hablar(self, msj):
        self.hablando = True
        mensaje = msj
        
        if self.hablando:
            print(mensaje)
    
    def correr(self):
        self.corriendo = True  
```

de tal manera, una vez que instanciamos la clase _persona_ (_i.e._ creamos un objeto de dicha clase) y llamamos al método ``hablar()`` pasándole un parámetro, entonces dicho método nos mostrará en pantalla el mensaje que pasamos por parámetro. Veamos


```python
# creamos un objeto

Luis = Persona()

# llamamos al método hablar()

Luis.hablar('Hola, te estoy saludando')
```

    Hola, te estoy saludando


## Método \__init\__ <a id="parte2"></a>

Por otro lado, a las primeras líneas de código dentro de nuestra clase hacen referencia a características comunes que tendrán (por defecto) nuestros objetos

```python
    # De manera simple podemos agregar estos atributos
    
    ojos = 2
    brazos = 2
    piernas = 2
    nariz = 1
    hablando = False
    corriendo = False
```

y que se conoce como **estado inicial**, el cual es ejecutado inmediatamente después de instanciar la clase.

A dicho estado inicial lo especificaremos mediante un **constructor** (define la forma en que se crean los objetos). En otras palabras, el **constructor** es un método especial que le da un estado inicial a los objetos. Ahora bien, trabajando con nuestro ejemplo podemos adaptar el código anterior para crear un método **constructor**, para ello utilizaremos la sintaxis básica

```python
def __init__(self):
```

que indica justamente que estamos creando un método constructor. Así, podemos adaptar el código de nuestro ejemplo como sigue

```python
    # Creamos el constructor 
    
      def __init__(self):
        self.ojos = 2
        self.brazos = 2
        self.piernas = 2
        self.nariz = 1
        self.hablando = False
        self.corriendo = False
```

Más aún, como ya vimos en la parte inicial de esta sesión podemos colocar parámetros a los métodos. Por ello podemos agregar como un atributo inicial a la clase _Persona_ el nombre que pueda llegar a tomar cada objeto de dicha clase, entre otras cosas más: 


```python
# Creamos la clase Persona 

class Persona():
    
    # Creamos el constructor (método inicializador)
    
    def __init__(self, nombre):
        self.nombre = nombre
        self.ojos = 2
        self.brazos = 2
        self.piernas = 2
        self.nariz = 1
        self.hablando = False
        self.corriendo = False
    
    # Después los siguientes métodos
    
    # agregamos un parámetro
    def hablar(self, msj):
        self.hablando = True
        mensaje = msj
        
        if self.hablando:
            print(mensaje)
    
    def correr(self):
        self.corriendo = True 
```

Observemos el código ``self.nombre = nombre`` en el cual ``self.nombre`` hace referencia a un atributo y ``nombre`` a la derecha del símbolo ``=`` hace alusión al parámetro del método. Luego, para instanciar una clase deberemos dar un valor correspondiente al parámetro del constructor, por ejemplo 


```python
# Creamos un objeto de la clase Persona

Luis = Persona('Luis')

# accedamos al atributo self.nombre

print(Luis.nombre)
```

    Luis


Finalmente creemos otro objeto:


```python
Eva = Persona('Eva')

print(Eva.nombre)

# accedemos a un atributo

print(Eva.hablando)

# invocamos el método hablar

Eva.hablar(f'Hola, mi nombre es {Eva.nombre}')

print(Eva.hablando)
```

    Eva
    False
    Hola, mi nombre es Eva
    True

