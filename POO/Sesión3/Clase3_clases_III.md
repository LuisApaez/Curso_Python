# Curso de introducción a la programación con Python

**Autor: Luis Fernando Apáez Álvarez**

## Clase 3:  Clases y objetos (Parte II)

* [Modificando los atributos de un objeto](#parte1)
    * [Nuevos atributos](#parte2)

## Modificando los atributos de un objeto <a id="parte1"></a>

Recordemos de la sesión pasada el código de la clase _Persona_: 


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
        
# Creamos un objeto de esta clase
Luis = Persona('Luis')
```

Ahora bien, sabemos que podemos acceder a los atributos iniciales (dados por el constructor) utilizando la nomenclatura del punto. Por ejemplo


```python
print(f'Hola, soy {Luis.nombre}')
```

    Hola, soy Luis

además

```python
# accediendo a un atributo de la clase persona

print(Luis.ojos)
```

    2


Luego, de la misma forma en que podemos acceder a los atributos de un objeto podemos modificarlos utilizando también la nomenclatura del punto. Por ejemplo podemos cambiar el atributo ``nombre`` del objeto ``Luis``


```python
# modificando el atributo nombre

Luis.nombre = 'Luis Fernando'

# veamos el resultado

print(Luis.nombre)
```

    Luis Fernando

luego

```python
# modificando el atributo corriendo de False a True

Luis.corriendo = True

# veamos el resultado

print(Luis.corriendo)
```

    True


Por otro lado, recordemos que para invocar un método escribíamos


```python
Luis.correr()

print(Luis.corriendo)
```

    True


pero existe una alternativa para ejecutar la misma acción, donde colocaremos primero el nombre de la clase, después el nombre del método y como parámetro de éste el objeto el cual deseamos que invoque dicho método (claro está, utilizando la nomenclatura del punto). Esto es


```python
# nombre de la clase/ nombre del método/ como parámetro el objeto que invoca el método
Persona.correr(Luis)

print(Luis.corriendo)
```

    True


Sin embargo esta última forma no es tan común de emplearse por lo que seguiremos trabajando con la primera manera. 

### Nuevos atributos <a id="parte2"></a>

Además de los atributos ya dados en el constructor, podemos agregar nuevos atributos. Por ejemplo, podemos agregar el atributo ``edad`` al objeto ``Luis`` como sigue


```python
# agregando un atributo nuevo al objeto Luis

Luis.edad = 23

print(f'La edad de {Luis.nombre} es de {Luis.edad} años')
```

    La edad de Luis Fernando es de 23 años


Sin embargo, el atributo nuevo que hemos agregado al objeto ``Luis`` no estará disponible para los demás objetos:


```python
# creamos un objeto nuevo de la clase Persona

Eva = Persona('Eva')

print(Eva.edad)
```


    ---------------------------------------------------------------------------
    
    AttributeError                            Traceback (most recent call last)
    
    <ipython-input-11-540d88242dd6> in <module>
          3 Eva = Persona('Eva')
          4 
    ----> 5 print(Eva.edad)


    AttributeError: 'Persona' object has no attribute 'edad'


Finalmente, es preciso mencionar que la modificación de los atributos a los dados originalmente no es una práctica muy deseable en muchos casos. Por ejemplo, si consideramos el atributo ``self.nariz = 1`` y después lo modificamos


```python
Luis.nariz = 4

print(Luis.nariz)
```

    4


sería una acción que no tendría mucho sentido y que no debería de permitirse. Para ello utilizaremos el concepto de _encapsulamiento_ el cual abordaremos en las siguientes sesiones.
