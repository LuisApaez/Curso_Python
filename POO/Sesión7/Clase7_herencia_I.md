# Curso de introducción a la programación con Python

**Autor: Luis Fernando Apáez Álvarez**

## Clase 7: Introducción a la _Herencia_

* [Primeros conceptos](#parte1)  
* [Clase _Abuelo_](#parte2)  
    * [Clase _Hijo_](#parte3)  

## Primeros conceptos <a id="parte1"></a>

El concepto de _Herencia_ dentro de la POO mantiene la misma idea básica que conocemos del lenguaje común. Por ejemplo, si nos basamos en el árbol genealógico de una persona, podemos decir que el _abuelo_ tiene ciertas características marcadas que heredará a sus hijos, y éstos a su vez a sus hijos; de tal manera el _abuelo_ hereda a sus hijos y a sus nietos ciertas características.

![Captura.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión7\Captura1.PNG)

Donde claramente la _herencia_ tiene un orden descendente y se basa en niveles jerárquicos (con el _abuelo_ en el primer nivel, su hijo en el segundo nivel y los nietos en el tercer nivel). Lo anterior representa un ejemplo de _herencia_ entre personas, pero podemos llevarlo a un ejemplo de _herencia_ dentro de un lenguaje de programación. Para ello sustituiremos los nombres abuelo, hijo y nietos por **clases**

![Captura1.PNG](C:\Users\weeee\OneDrive\Datos adjuntos\Documentos\Documentos(A)\Softwares\Python\Curso_introducción\POO\Sesión7\Captura2.PNG)

representadas también dentro de un sistema jerárquico; siendo así que las clases pueden heredar características (atributos y/o métodos) de otras clases. De lo anterior podemos decir que a la ``clase 1`` se le denomina **superclase**, a la ``clase 2`` **subclase** de la ``clase 1`` (simultáneamente, a la ``clase 2`` se le puede denominar superclase de las ``clase 2`` y ``clase 3``); de la misma manera, a la ``clase 3`` y ``clase 4`` las denominamos subclases.

Por otro lado, la _herencia_ dentro de la POO sirve para

* Definir nuevas clases basándonos en algunas ya existentes, de modo que podemos **reutilizar** código.

* Mantener el código mucho más limpio, estructurado y con menos líneas, siendo así éste más eficiente.

## Clase _Abuelo_ <a id="parte2"></a>

Una vez entendidos los primeros conceptos sobre la _herencia_ podemos trabajar el código para crear la superclase _Abuelo_ y la subclase _Hijo_, intentando trasladar el ejemplo de herencia entre personas a conceptos de programación. Para ello escribimos primero:


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
    
        self.hablando = False
        self.corriendo = False
    
    # ------------------------------------------
    
    # Después los siguientes métodos
    
    def hablar(self, msj):
        self.hablando = True
        mensaje = msj
        
        if self.hablando:
            print(mensaje)
    
    def correr(self):
        self.corriendo = True 
```

Posteriormente creamos la subclase _Hijo_ la cual heredara los atributos y métodos de la clase _Abuelo_. Debemos aclarar dos puntos

1. Trivialmente podemos decir que la subclase _hijo_ hereda los métodos ``hablar()`` y ``correr()`` pues así ocurre en la mayoría de los casos con los hijos.
2. Podemos decir que la clase _hijo_ hereda algunos de los atributos marcados en el constructor de la clase _Abuelo_, lo cual si pasa en la herencia entre personas. Por ejemplo, es común que el hijo herede alguna característica del padre, ya sea el color de tez, el color de ojos o de cabello; lo que es claro que el hijo heredará es el apellido paterno. Sin embargo, podemos pensar también que la clase _hijo_ no tendrá el mismo valor en el atributo ``self.color_ojos``, de modo que deberemos realizar las correcciones necesarias para abordar este caso.

Ahora bien, creamos la clase _Hijo_ que por el momento no haga nada

```python
# Creamos la clase Hijo

class Hijo():
    pass
```

para declarar que la clase _Hijo_ es una subclase de la clase _Abuelo_, bastará con colocar como parámetro de la clase _Hijo_ el nombre de la superclase en cuestión, esto es


```python
# Creamos la clase Hijo como subclase de la clase Abuelo

class Hijo(Abuelo):
    pass
```

Además, cuando instanciemos esta clase deberemos de pasar también un parámetro (``nombre``) que exige el constructor de la clase _Abuelo_ pues recordemos que la subclase _Hijo_ hereda los atributos y métodos de la superclase _Abuelo_. Veamos pues que


```python
# Instanciamos la clase Hijo

Pedro = Hijo('Pedro')

# Veamos todos los atributos heredados
print('-' * 30)

print(f'Apellido de {Pedro.nombre}: {Pedro.apellido}')
print(f'Color de ojos de {Pedro.nombre}: {Pedro.color_ojos}')
print(f'Color de cabello {Pedro.nombre}: {Pedro.color_cabello}')
print(f'Tez de {Pedro.nombre}: {Pedro.tez}')

print('-' * 30)

#Método hablar() heredado
Pedro.hablar('Hola!')
```

    ------------------------------
    Apellido de Pedro: Apáez
    Color de ojos de Pedro: negro
    Color de cabello Pedro: marrón
    Tez de Pedro: morena
    ------------------------------
    Hola!


Suponiendo que el color de ojos de ``Pedro`` es verde en vez de negro, entonces podemos modificar el valor del atributo ``self.color_ojos`` como sabemos hacerlo:


```python
# Modificando el atributo de color de ojos
Pedro.color_ojos = 'verdes'

# Veamos el resultadob
print(Pedro.color_ojos)
```

    verdes


el cual sólo se verá afectado en el objeto ``Pedro`` y no en los demás objetos. Por ejemplo


```python
# Creamos otro objeto de la clase Hijo
Lalo = Hijo('Lalo')

# Veamos el color de ojos de Lalo
print(Lalo.color_ojos)
```

## Clase _Hijo_ <a id="parte3"></a>

Hasta ahora ya hemos visto como atributos y métodos son heredados a la subclase _Hijo_ provenientes de la superclase _Abuelo_; asimismo, observamos que ciertos atributos de la clase _Abuelo_ son distintos en la clase _Hijo_, donde realizamos (por ejemplo) la modificación pertinente en un objeto en especifico. Posteriormente veremos que la propia clase _Hijo_ puede tener atributos adicionales a los heredados, así como métodos.

Por ende, comenzaremos modificando la clase _Hijo_ agregándole algunos otros atributos y métodos:

```python
# Creamos la clase Hijo como subclase de la clase Abuelo

class Hijo(Abuelo):
    
    # Constructor
    def __init__(self, num_celular):
        
        # Atributos
        self.num_celular = num_celular
        self.idiomas = ['Inglés', 'Francés', 'Italianos']
        self.estudiar = False
        
    # Métodos
    def ir_escuela(self):
        self.estudiar = True
        print('Voy camino a la escuela')
```

sin embargo el código anterior aún está incompleto. Si bien hemos escrito ``class Hijo(Abuelo)`` para hacer referencia a que la clase _Hijo_ es subclase de la clase _Abuelo_, notemos que la propia clase _Hijo_ tiene un constructor, donde recordemos que esta subclase hereda el constructor de la clase _Abuelo_, por lo que tenemos un pequeño problema respecto a los parámetros de este constructor. Para arreglar el problema debemos de escribir

```python
    # Constructor:
    # Agregamos el parámetro (o los parámetros) del constructor de la superclase
    
    def __init__(self, nombre, num_celular):
        
        # hacemos referencia de los parámetros de la superclase 
        super().__init__(nombre)
        
        # Atributos
        self.num_celular = num_celular
        self.idiomas = ['Inglés', 'Francés', 'Italianos']
        self.estudiar = False
```

con lo cual tendremos que

* En el constructor de la subclase debemos colocar los parámetros marcados en el constructor de la superclase.

* Seguido de lo anterior debemos emplear ``super().__init__()`` para marcar dentro del constructor de la subclase cuáles parámetros son referentes al constructor de la superclase. Por ello nosotros colocamos ``super().__init__(nombre)`` pues en la superclase _Abuelo_ el único parámetro que tiene su respectivo constructor es ``nombre``.

De tal manera, cuando instanciemos la clase _Hijo_ deberemos ingresar dos parámetros: el primero será un valor para el parámetro ``nombre`` declarado en el constructor de la superclase _abuelo_ y el segundo será un valor para el parámetro ``num_celular`` declarado en el propio constructor de la clase _Hijo_. Veamos


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
        self.estudiar = False
        self.pedalear = False
        
    # Métodos
    def ir_escuela(self):
        self.estudiar = True
        print('Voy camino a la escuela')
        
    def andar_bici(self):
        self.pedalear = True
```


```python
# Creamos otro objeto de la clase Hijo

Zin = Hijo('Zin', '520-1789')
```

luego observemos los atributos y métodos propios de la clase _Hijo_ mediante el objeto ``Zin``:


```python
# Atributo heredado
print(f'Algunos datos sobre {Zin.nombre}')
print('-' * 30)

# Atributos propios

print(f'El número telefónico: {Zin.num_celular}')
print(f'Idiomas en estudio: {Zin.idiomas}')
print(f'¿Pedaleando? : {Zin.pedalear}')
print(f'¿Estudiando? : {Zin.estudiar}')
print('-' * 30)

# Métodos propios

Zin.andar_bici()
print(f'¿Pedalenado? : {Zin.pedalear}')

Zin.ir_escuela()
print(f'¿Estudiando? : {Zin.estudiar}')

# Método heredado
Zin.hablar('Hola!!')
```

    Algunos datos sobre Zin
    ------------------------------
    El número telefónico: 520-1789
    Idiomas en estudio: ['Inglés', 'Francés', 'Italianos']
    ¿Pedaleando? : False
    ¿Estudiando? : False
    ------------------------------
    ¿Pedalenado? : True
    Voy camino a la escuela
    ¿Estudiando? : True
    Hola!!

