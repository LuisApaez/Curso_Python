# Curso de introducción a la programación con Python

**Autor: Luis Fernando Apáez Álvarez**

## Clase 6: Conceptos adicionales

* [Atributos de sólo lectura](#parte1)  
* [Mensaje final sobre Get y Set ](#parte2)  
* [Métodos especiales](#parte3)
    * [Destructor de Objetos](#parte4)
    * [Método para mostrar objetos](#parte5)

## Atributos de sólo lectura <a id="parte1"></a>

Retomando el código de la clase _Punto_ visto en la sesión anterior


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

cuando tenemos atributos encapsulados y los métodos ``get`` y ``set`` asociados, podemos convertir a dicho atributo en un atributo de sólo lectura si quitamos la parte del método ``set`` en nuestro código. Lo cual es totalmente lógico pues el método ``set`` es el que nos permite la modificación del atributo, a diferencia del método ``get`` el cual nos permite "leer" dicho atributo.

Por ende, los atributos de sólo lectura son atributos encapsulados que carecen de un método ``set`` para modificarlos.

## Mensaje final sobre Get y Set <a id="parte2"></a>

Después de poner en práctica el conocimiento adquirido sobre los métodos ``get`` y ``set`` y sobre el encapsulamiento de atributos y métodos en <span style="color:rgb(10,10,150)">Python</span>, es necesario recordar dos hechos importantes:

<ol>
<li>Para declarar un atributo (o método) privado  existe la convención en <span style="color:rgb(10,10,150)">Python</span> de utilizar un guión bajo como prefijo al nombre del atributo, sin embargo, al realizar esta acción no se garantiza la encapsulación propiamente, pues podemos acceder de forma usual a dicho atributo (o método) y modificarlo. Más bien este guión bajo funge como indicador, para el desarrollador, que dicho atributo (o método) debe tratarse como privado. </li>
<li>Originalmente el doble guión bajo tiene otra función dentro de <span style="color:rgb(10,10,150)">Python</span> que la que le hemos dado, es decir, el doble guión bajo no es propiamente para la encapsulación, aunque así lo hemos tratado con fines ilustrativos. De hecho, la parte referente a los métodos ``get`` y ``set`` (y en general sobre la encapsulación en <span style="color:rgb(10,10,150)">Python</span>) tiene como fin dar un tratamiento decente sobre estos métodos en la programación orientada a objetos, pues en <span style="color:rgb(10,10,150)">Python</span> estos temas están de más dada su naturaleza. 
Por ejemplo podemos recordar nuevamente el código de la clase <i>Punto</i>
</li>    
</ol>

```python
# Definimos la clase Punto

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

el cual, dentro de <span style="color:rgb(10,10,150)">Python</span>, es totalmente equivalente a 
    
```python
# Definimos al clase Punto

class Punto():
    
    # Creamos el constructor
    def __init__(self, x, y):
        
        # Atributos de la clase
        self.x = x
        self.y = y   
```

siendo éste último más eficiente respecto al primero, donde ambas versiones del código de la clase realizan las mismas funcionalidades.


Por ende, utilizar ``getters`` y ``setters`` dentro de <span style="color:rgb(10,10,150)">Python</span> es redundante. En lo que sigue, y cuando sea necesario, el tratamiento de los atributos privados se adaptará a la convención de utilizar un solo guión bajo y sin manejar ``getters`` y ``setters``; sin embargo, el conocimiento que adquirimos no será en vano, pues el tratamiento expuesto sobre dichos métodos y sobre la encapsulación es muy útil dentro de otros lenguajes de programación, tales como <span style="color:rgb(200,10,10)">Java</span>.

## Métodos especiales <a id="parte3"></a>

Retomemos el código simplificado de la clase _Punto_ (sin todo el enrollo de los ``getters`` y ``setters``):


```python
# Definimos al clase Punto
class Punto():
    
    # Creamos el constructor
    def __init__(self, x, y):
        
        # Atributos de la clase
        self.x = x
        self.y = y  
```

Como vimos en las primeras sesiones sobre _Clases y Objetos_ el método ``__init__`` es un método especial y tiene el papel de ser el **contructor** de la clase. Así como el método ``__init__``, tenemos otros tipos de métodos especiales.

### Destructor de objetos<a id="parte4"></a>

El método _Destructor de objetos_ (``__del__``) es llamado cuando la instancia será borrada. De tal manera podemos ejecutar ciertas acciones, según sea el caso, cuando nuestro objeto es borrado.

Cabe resaltar que eliminar y borrar son conceptos distintos pues, si eliminamos un objeto lo que conseguimos hacer es ir disminuyendo el número de referencias sobre sobre él y cuando dicho número de referencias llegue a cero, entonces el método destructor ``__del__`` será llamado, desencadenando las acciones que previamente hemos definido en él y realizando lo mínimo imprescindible en cuanto a la limpieza del objeto. De tal manera, el método es útil si es de nuestro interés liberar recursos de la memoria.

Por ejemplo podemos implementar un método destructor para que retorne un mensaje una vez que el objeto ha sido borrado


```python
# Definimos al clase Punto
class Punto():
    
    # Creamos el constructor
    def __init__(self, x, y):
        
        # Atributos de la clase
        self.x = x
        self.y = y  
        
    # Creamos el desctructor
    def __del__(self):
        print(f'El punto {self.x, self.y} ha sido borrado')
```


```python
# Creamos un objeto de la clase Punto
p1 = Punto(2,1)

print('Destrucción del objeto'.center(30,'-'))

# Probamos el método destructor
del p1
```

    ----Destrucción del objeto----
    El punto (2, 1) ha sido borrado


No obstante, en <span style="color:rgb(10,10,150)">Python</span> existe algo denominado _recolector de basura_ el cual hace la limpieza correspondiente en la memoria de variables a las cuales no se les está apuntando, es decir variables que tienen cero número de referencias. Es por ello que este método especial es poco común dentro de <span style="color:rgb(10,10,150)">Python</span>. 

### Método para mostrar objetos<a id="parte5"></a>

Recordemos de la práctica 2 que, cuando creamos el código de la clase _Punto_, definimos un método para mostrar el punto que se crea una vez instanciamos la clase

```python
# Creamos un método para mostrar el punto ingresado

    def mostrar(self):
        return f'({self.__x},{self.__y})'
```

Ahora bien, para el caso especifico de **mostrar** objetos en <span style="color:rgb(10,10,150)">Python</span> tenemos un método especial denominado ``__str__``, el cual debe devolver una cadena de carácteres con lo que queremos mostrar. Es así como el método ``__str__`` retorna una cadena que puede ser usada para representar apropiadamente información sobre la clase.

Por ejemplo, en vez de utilizar el método ``mostrar()`` que usamos en la práctica 2, podemos implementar un método ``__str__`` como


```python
# Definimos al clase Punto
class Punto():
    
    # Creamos el constructor
    def __init__(self, x, y):
        
        # Atributos de la clase
        self.x = x
        self.y = y 
        
    # Creamos el método para mostrar objetos
    def __str__(self):
        return f'({self.x}, {self.y})'
```


```python
# Creamos un objeto de la clase Punto
p2 = Punto(-1,1)

# Invocamos el método __str__ utilizando str()
str(p2)
```




    '(-1, 1)'




```python
# o alternativamente podemos escribir simplemente

print(p2)
```

    (-1, 1)


Es importante recalcar que el método ``__str__`` sólo devuelve cadenas de texto.
