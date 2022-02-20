## Curso de introducción a la programación con Python

**Autor: Luis Fernando Apáez Álvarez**

## Clase4: Encapsulamiento

* [Encapsulando atributos](#parte1)

Comenzaremos viendo un ejemplo de una clase, la cual calculará el área de un rectángulo. Para ello


```python
# Definimos la clase

class Area():
    
    # Definimos el método inicializador
    def __init__(self, b, a, nombre):
        self.nombre = nombre
        self.base = b
        self.altura = a
        
    # Creamos un método para calcular el área
    def calcular(self):
        return self.base * self.altura

# Creamos un objeto de la clase Area
r1 = Area(5, 4, 'Rectángulo 1')

# Calculamos su área
print(f'El área del {r1.nombre} es: {r1.calcular()}')
```

    El área del Rectángulo 1 es: 20
    

Ahora bien, como mencionamos en la clase pasada, no es una buena práctica permitir la modificación de atributos, como por ejemplo


```python
r1.base = 7

print(r1.base)
```

    7
    

pues en muchos casos realizar estas acciones podrá traer grandes problemas en el resto del código. Por ejemplo, al calcular ahora el área del rectángulo tendremos que ésta ha cambiado


```python
print(r1.calcular())
```

    28
    

la cual ya no representa el área del ``rectángulo 1`` el cual tiene de dimensiones $base = 5$ y $altura=4$. 

De tal manera surge la necesidad de proteger (o _encapsular_) una propiedad para que no que pueda modificarse desde fuera de la clase.

## Encapsulando atributos <a id="parte1"></a>

Ahora bien, hasta el momento, los atributos que hemos manejado en nuestras clases se conocen como _atributos públicos_, los cuales pueden se consultados y/o modificados fuera de la propia clase. Si deseamos tener atributos que sólo puedan usarse o modificarse dentro de la clase, es decir de _atributos privados_, entonces utilizaremos un guón bajo como prefijo al atributo. Por ejemplo, podemos modificar el código de nuestro ejemplo inicial para hacer que los atributos en el constructor sean privados: 


```python
# Definimos la clase

class Area():
    
    # Definimos el método inicializador
    def __init__(self, b, a, nombre):
        
        # Definimos los atributos como privados agregando (_)
        self._nombre = nombre
        self._base = b
        self._altura = a
        
    # Creamos un método para calcular el área
    def calcular(self):
        
        # Para utilizar los atributos en otros métodos
        # dentro de la clase debemos de usar también el guión bajo
        return self._base * self._altura
```

de esta manera indicaremos a cualquier desarrollador que dichos atributos deben de tratarse como privados y que no deben de ser expuestos o modificados externamente. Cabe aclarar que lo anterior es tan sólo una convención pues, de hecho, aún después de hacer que los atributos sean privados agregando el guión bajo podemos modificarlos externamente. Por ejemplo


```python
# Creamos un objeto de la clase Area

r1 = Area(5, 4, 'Rectángulo 1')

# veamos el valor de los atributos de dicho objeto
# (no debemos olvidar que ahora hay que poner un guión bajo como prefijo)

print(f'La base de {r1._nombre} es {r1._base} y la altura es de {r1._altura}')
```

    La base de Rectángulo 1 es 5 y la altura es de 4
    


```python
# podemos modificar los atributos desde fuera de la clase
# aún cuando hemos declarado que son privados

r1._nombre = 'Rec 1'
print(r1._nombre)
```

    Rec 1
    

El detalle radica en que para <span style="color:rgb(10,10,150)">Python</span> no hay como tal atributos públicos o privados, de tal manera el guión bajo funge como una convención para el intento de manejo de los atributos privados y para trabajar con éstos.

Existe una alternativa para evitar (ahora si) el acceso y modificación de los atributos fuera de la propia clase, la cual radica en colocar doble guión bajo como prefijo. Aunque la función original del doble guión bajo no es la encapsulación, es muy frecuente su utilización para dicho fin. Veamos 


```python
# Definimos la clase

class Area():
    
    # Definimos el método inicializador
    def __init__(self, b, a, nombre):
        
        # Definimos los atributos como privados agregando (__)
        # de modo que no podrán accederlos fuera de esta clase
        
        self._nombre = nombre
        self.__base = b
        self.__altura = a
        
    # Creamos un método para calcular el área
    def calcular(self):
        
        # Para utilizar los atributos en otros métodos
        # dentro de la clase debemos de usar también el doble guión bajo
        return self.__base * self.__altura
```

con lo anterior no podremos acceder a los atributos ``base`` y ``altura`` con lo cual, al intentar acceder a ellos, obtendremos un error


```python
# Creamos un objeto de la clase Area

r2 = Area(2, 1, 'Rectángulo 2')

print(r2.__base)
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-20-4dc7898e9991> in <module>
          3 r2 = Area(2, 1, 'Rectángulo 2')
          4 
    ----> 5 print(r2.__base)
    

    AttributeError: 'Area' object has no attribute '__base'


sin embargo si podremos conocer el área de dicho rectángulo, de modo que los atributos dentro de la propia clase funcionan de forma habitual


```python
print(r2.calcular())
```

    2
    

Si bien lo anterior puede presentar como primer inconveniente el no poder "ver" los valores de los atributos de nuestro objeto ``r2``, podemos solucionarlo creando un método para mostrarlos:


```python
# Definimos la clase

class Area():
    
    # Definimos el método inicializador
    def __init__(self, b, a, nombre):
        
        # Definimos los atributos como privados agregando (__)
        # de modo que no podrán accederlos fuera de esta clase
        
        self._nombre = nombre
        self.__base = b
        self.__altura = a
        
    # Creamos un método para mostrar los atributos "encapsulados"
    def mostrar_atributos(self):
        print(f'La dimensión de la base de {self._nombre} es b = {self.__base}')
        print(f'La dimensión de la altura de {self._nombre} es a = {self.__altura}')
        
    # Creamos un método para calcular el área
    def calcular(self):
        
        # Para utilizar los atributos en otros métodos
        # dentro de la clase debemos de usar también el doble guión bajo
        return self.__base * self.__altura
```


```python
# Creamos un objeto de la clase Area

r2 = Area(2, 1, 'Rectángulo 2')

# veamos el valor de los atributos por medio del método mostrar()
r2.mostrar_atributos()
```

    La dimensión de la base de Rectángulo 2 es b = 2
    La dimensión de la altura de Rectángulo 2 es a = 1
    

Para finalizar es preciso mencionar que las variables ``r2.base``, ``r2._base`` y ``r2.__base`` son todas distintas y sólo ``r2.__base`` hace alusión al atributo definido de la clase.
