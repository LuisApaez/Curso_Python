## Curso de introducción a la programación con Python

**Autor: Luis Fernando Apáez Álvarez**

## Clase 5: Método Get y Set

* [Métodos Get y Set en Python](#parte1)
    * [Decorador @Property](#parte2)  

Comencemos por retomar el código de la clase _Area_ de la sesión pasada:


```python
# Definimos la clase

class Area():
    
    # Definimos el método inicializador
    def __init__(self, b, a, nombre):
        
        # Definimos los atributos como privados agregando (__)
        
        self.__nombre = nombre
        self.__base = b
        self.__altura = a
        
    # Creamos un método para mostrar los atributos encapsulados
    def mostrar_atributos(self):
        print(f'La dimensión de la base de {self.__nombre} es b = {self.__base}')
        print(f'La dimensión de la altura de {self.__nombre} es a = {self.__altura}')
        
    # Creamos un método para calcular el área
    def calcular(self):
        
        # Para utilizar los atributos en otros métodos
        # dentro de la clase debemos de usar también el doble guión bajo
        return self.__base * self.__altura
```

donde, para poder ver los atributos encapsulados creamos el método ``mostrar_atributos()``, no obstante, existe una manera más propia de realizar dicha acción. Más aún, con los métodos que veremos a continuación podremos acceder y modificar los atributos encapsulados; de tal manera, estos métodos se utilizan por la necesidad de acceder y modificar atributos privados.

## Métodos Get y Set en Python <a id="parte1"></a>

El método _get_ (obtener/recuperar) nos permitirá retornar el valor de una variable encapsulada y el método _set_ (fijar) modificar el valor de dicha variable. Estos métodos surgen de la necesidad de poder acceder y modificar variables (o métodos) encapsuladas cuando así lo necesitemos.

Comencemos trabajando con la clase _Punto_:


```python
# Definimos la clase Punto

class Punto():
    
    # Creamos el constructor
    def __init__(self, x, y):
        
        # Los atributos deberán estar encapsulados
        self.__x = x
        self.__y = y
        
    # Creamos el método get para retornar los atributos
    def x(self):
        return self.__x
    
    def y(self):
        return self.__y
    
    # Creamos el método set para modificar el valor de los atributos
    # (aquí el nombre set_x del método sólo es ilustrativo pues en realidad
    # éste puede llamarse como sea) 
    
    def set_x(self, x):
        self.__x = x
        
    def set_y(self, y):
        self.__y = y
```


```python
# Creamos un objeto de la clase Punto

p1 = Punto(0,0)

# veamos sus atributos por medio del método get

print(p1.x())
print(p1.y())
```

    0
    0


versus

```python
print(p1.x)
print(p1.y)
```

que escribiríamos si los atributos en el constructor de nuestra clase no estuvieran encapsulados. Continuando


```python
# podemos modificar el valor de los atributos a través del método set

p1.set_x(2)
p1.set_y(6)

print(p1.x())
print(p1.y())
```

    2
    6


versus

```python
p1.x = 2
p1.y = 6

print(p1.x)
print(p1.y)
```

que escribiríamos si los atributos en el constructor de nuestra clase no estuvieran encapsulados.

### Decorador @Property <a id="parte2"></a>

Un decorador es un patrón de software que se utiliza para alterar el funcionamiento de una determinada pieza de código.
El decorador ``@property`` se utiliza para modificar un método, para que éste se convierta en un atributo o propiedad. Suele ocuparse cuando se trabaja con los métodos ``get`` y ``set``.

Cuando encapsulamos una variable deseamos que no sea accesible desde el exterior de una manera no controlada, al utilizar un método ``get`` en conjunto con el decorador ``@property`` podremos tratar a dicho método como un atributo. La ventaja de esto es que el acceso a dicho atributo será a través de una función (en específico del método ``get``) el cual provee de un acceso controlado. Ahora bien, podemos modificar ahora la parte del ``set``:

```python
    def set_x(self, x):
        self.__x = x
        
    def set_y(self, y):
        self.__y = y
```

valiéndonos de otro decorador que haga referencia, justamente, al método ``set``. Para ello utilizaremos un decorador que llevará el nombre del atributo (sin guiones bajos) y la palabra ``setter`` utilizando la nomenclatura del punto. Esto es 

```python
    @x.setter
    def x(self, x):
        self.__x = x
    
    @y.setter
    def y(self, y):
        self.__y = y
```
De tal manera podemos modificar el código de la clase _Punto_ como sigue 


```python
# Definimos al clase Punto

class Punto():
    
    # Creamos el constructor
    def __init__(self, x, y):
        
        # Los atributos deberán estar encapsulados
        self.__x = x
        self.__y = y
        
    # Creamos el método get para retornar los atributos en conjunto
    # del decorador Property
    
    @property
    def x(self):
        return self.__x
    
    @property
    def y(self):
        return self.__y
    
    # Creamos el método set para modificar el valor de los atributos
    # en conjunto del decorador nombre_del_atributo.setter
    
    @x.setter
    def x(self, x):
        self.__x = x
    
    @y.setter
    def y(self, y):
        self.__y = y
```

Es gracias a los decoradores que conseguimos distinguir entre las funcionalidades de los métodos ``get`` y ``set``, pues sin éstos caeríamos en el peligro de trabajar con una misma función que realice dos cosas distintas, además una de ellas no pasa parámetros y la otra si. Ahora bien


```python
# Creamos un objeto de la clase Punto

p1 = Punto(0,0)

# veamos sus atributos por medio del método get

print(p1.x)
print(p1.y)
```

    0
    0


versus 

```python
print(p1.x())
print(p1.y())
```

que escribíamos sin utilizar decoradores. Continuando


```python
# podemos modificar el valor de los atributos a través del método set

p1.x = 2
p1.y = 6

print(p1.x)
print(p1.y)
```

    2
    6


versus 

```python
p1.set_x(2)
p1.set_y(6)

print(p1.x())
print(p1.y())
```

que escribíamos sin utilizar el decorador ``nombre_del_atributo.setter``. Finalmente, podemos modificar el código de la clase _Area_ implementando el conocimiento que hemos adquirido: 


```python
# Definimos la clase

class Area():
    
    # Definimos el método inicializador
    def __init__(self, b, a, nombre):
        
        # Definimos los atributos como privados agregando (__)
        
        self.__nombre = nombre
        self.__base = b
        self.__altura = a
        
    # Implementamos los getters
    @property
    def nombre(self):
        return self.__nombre
        
    @property 
    def base(self):
        return self.__base

    @property
    def altura(self):
        return self.__altura
    
    # Implemenatamos los setters
    @nombre.setter
    def nombre(self, nombre):
        self.__nombre = nombre
    
    @base.setter
    def base(self, b):
        self.__base = b

    @altura.setter
    def altura(self, a):
        self.__altura = a
        
    # Creamos un método para calcular el área
    def calcular(self):
        
        # Para utilizar los atributos en otros métodos
        # dentro de la clase debemos de usar también el doble guión bajo
        return self.__base * self.__altura
```


```python
# Creamos un objeto de la clase Area
r1 = Area(5,4, 'Rectángulo 1')

# Accedemos a sus atributos
print(r1.nombre)
print(r1.base)
print(r1.altura)

# Calculamos el área
print(r1.calcular())
```

    Rectángulo 1
    5
    4
    20

y

```python
# Modificamos los atributos por medio de los setter

r1.nombre = 'Rec 1'
r1.base = 7
r1.altura = 8

# Accedemos a sus atributos
print(r1.nombre)
print(r1.base)
print(r1.altura)

# Calculamos el área
print(r1.calcular())
```

    Rec 1
    7
    8
    56

