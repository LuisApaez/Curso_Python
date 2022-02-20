# Curso de introducción a la programación con Python

**Autor: Luis Fernando Apáez Álvarez**

## Clase 1:  Clases y objetos (Parte I)

* [Clases](#parte1)
    * [Terminología de una clase](#parte2)

La programación orientada a objetos busca trasladar la naturaleza de los objetos de la vida real al código de programación, donde estos objetos tienen un estado, comportamiento y propiedades. Esta forma de programar  permite estructurar el código en fragmentos simples y reutilizables. Dentro de ella se encuentran los conceptos de **clases y objetos** los cuales serán abordados en las primeras clases.


## Clases <a id="parte1"></a>

Una **clase** es uno de los bloques básicos de <span style="color:rgb(10,10,150)">python</span> además de ser un concepto primordial referente de la programación orientada a objetos.

Podemos pensar a una **clase** como una plantilla de la cual pueden crearse **instancias** u **objetos**. Por ejemplo, podemos pensar a una _persona_ como una clase y a un objeto de esta clase una persona en específico, digamos Luis de 23 años de la Ciudad de México. Cabe resaltar que todas las instancias u objetos de una clase poseen las mismas variables de datos pero con diferentes valores, de modo que otro objeto de la clase _persona_ puede ser Eva de 20 años de Guanajuato.

Ahora bien, crearemos nuestra primer clase siguiendo la sintaxis siguiente:


```python
# creamos la clase Persona

class Persona:
    pass
```

donde ``pass`` indica que nuestra clase no tiene contenido (por el momento). Veamos después que


```python
print(type(Persona))
```

    <class 'type'>

además

```python
# creamos un objeto de la clase Persona

Eva = Persona()

print(type(Eva))
```

    <class '__main__.Persona'>


indica justamente que ``Persona`` es una clase. Más adelante veremos más a detalle la construcción de una clase, sin embargo es preciso ver primero algo más de teoría.

### Terminología de una clase <a id="parte2"></a>

* Modularización: es una forma de organización de un programa en la que distintos componentes se dividen en unidades funcionales separadas. Por ejemplo podemos pensar un carro como un programa con muchas clases, desde la clase llantas hasta la clase estéreo, donde cada una de estas clases puede funcionar de manera separada.

* Atributos: son la información referente de un objeto. Por ejemplo, dada la clase _persona_ y tomando una persona en específico como objeto, digamos Eva de 20 años de Guanajuato; tenemos que tanto el nombre, la edad y la ciudad son atributos (información) de dicho objeto.

* Métodos: son procedimientos definidos dentro del objeto. Para crear métodos dentro del objeto usaremos la palabra reservada ``def`` como la utilizabamos en funciones. La diferencia es que, la palabra ``def`` por sí sola es referente a las funciones, sin embargo, la palabra ``def`` dentro de una clase hará referencia a un método. La sintaxis básica de una método (función dentro de una clase) es:


```python
def nombre_funcion(self):
    pass
```

Como vimos líneas arriba, ``pass`` indica que el método no hace nada; luego ``self`` es un parámetro por defecto y que hace referencia al objeto perteneciente a dicha clase. Más adelante se irán aclarando más estos conceptos.

* Herencia: entre clases que se relacionen, las propiedades pueden transmitirse. Por ejemplo, de la clase _mamífero_ pueden heredarse propiedades a las clases _gato_ y _perro_, digamos por ejemplo la reproducción. De esta manera no es necesario crear el método reproducción para cada una de las clases _gato_ y _perro_ pues basta con generalizarlo en el método correspondiente a la clase _mamífero_ para poder heredarlo a otras clases.

* Encapsulamiento: 

* Polimorfismo: es la habilidad para los distintos objetos de una clase de responder al mismo método de manera distinta. Por ejemplo, podemos considerar la clase _animal_ y un método que indique la forma en que los objetos de dicha clase se comunican. De tal manera, empleando dicho método al objeto _perro_ dentro de la clase _animal_ tendremos un ladrido; empleando dicho método al objeto _gato_ dentro de la clase _animal_ tendremos un maullido, etcétera. Es así como los distintos objetos de la clase _animal_ tienen respuestas distintas respecto a un mismo método. 

* Más sobre un _objeto_: Para **acceder** a los atributos y métodos disponibles para un objeto utilizaremos la nomenclatura del punto. Por ejemplo, considerando a Luis como un objeto de la clase _persona_ podemos acceder a sus atributos utilizando 

```python
Luis.edad = 23
Luis.ciudad = ciudad de México
.
.
etcétera
```

así como acceder al comportamiento del objeto (métodos) como

```python
Luis.hablar()
Luis.correr()
.
.
etcétera
```

Una vez visto lo anterior podemos mejora el código de nuestra clase _persona_ agregando algunos atributos y métodos:


```python
# creamos la clase Persona 

class Persona():
    
    # de manera simple podemos agregar estos atributos
    ojos = 2
    brazos = 2
    piernas = 2
    nariz = 1
    hablando = False
    corriendo = False
    
    # después los siguientes métodos
    def hablar(self):
        self.hablando = True
    
    def correr(self):
        self.corriendo = True
    
# creamos un objeto para dicha clase

Luis = Persona()        

# lo anterior se conoce como instanciar una clase
```

después, podemos ver los atributos de dicho objeto recurriendo a la nomenclatura del punto


```python
print('Algunos atributos: ')

print(Luis.ojos)
print(Luis.nariz)

print('-' * 30)

print('Algunos comportamientos (métodos): ')

# aplicamos los métodos
Luis.hablar()
Luis.correr()

# veamos el resultado
print(Luis.hablando)
print(Luis.corriendo)
```

    Algunos atributos: 
    2
    1
    ------------------------------
    Algunos comportamientos (métodos): 
    True
    True


A partir de este punto podemos observar mejor como la declaración del método ``hablar()``

```python
    def hablar(self):
        self.hablando = True
```

dentro de nuestra clase toma como parámetro la palabra reservada ``self`` y la cual actúa de la siguiente manera:

* cuando accedemos al método ``hablar()`` mediante el objeto Luis utilizamos ``Luis.hablar()``
* así, el parámetro ``self`` en este caso toma el valor de ``Luis`` de modo que podemos ver actuar al método dentro de la clase como

```python
    def hablar(Luis):
        Luis.hablando = True
```

* es por ello que al ejecutar ``print(Luis.hablando)`` el resultado es ``True`` en vez de ``False`` como se declaraba en los atributos de la clase.
