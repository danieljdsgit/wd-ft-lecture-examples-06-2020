# Specificity

La regla más específica ganará. Si dos o más reglas tienen la misma especificidad, el que aparece último (en la hoja de estilos) gana.


## Cómo calcular la especificidad

La especificidad se calcula utilizando una convención.
Tenemos 4 posiciones, y cada uno de ellos comienza en 0: ```0 0 0 0 0```. La posición de la izquierda es la más
importante, y la de la derecha es la menos importante.
Al igual que funciona para los números en el sistema decimal: ```1 0 0 0``` es mayor que ```0 1 0 0```.

## Posición 1

La primer posición, la de más a la derecha, es la menos importante.
Aumentamos este valor cuando tenemos un selector de elementos. Si tienes más de un selector de elementos en la regla, se incrementa en consecuencia el valor almacenado en
esta posición.

Ejemplo:

```css
p {}             /* 0 0 0 1 */  
span {}          /* 0 0 0 1 */  
p span {}        /* 0 0 0 2 */  
p > span {}      /* 0 0 0 2 */  
div p > span {}  /* 0 0 0 3 */
```

## Posición 2

La segunda posición se incrementa por:
- selectores de clase
- selectores de pseudo-clase
- selectores de atributos  

Cada vez que una regla cumple con uno de esos, incrementamos el valor de la segunda columna desde la derecha.

Ejemplos:

```css
.name {}          /* 0 0 1 0 */
.users .name {}   /* 0 0 2 0 */
[href$='.pdf'] {} /* 0 0 1 0 */
:hover {}         /* 0 0 1 0 */
```

Por supuesto, los selectores de la posición 2 se pueden combinar con los selectores de la posición 1:

```css
div .name {}           /* 0 0 1 1 */
a[href$='.pdf'] {}     /* 0 0 1 1 */
.pictures img:hover {} /* 0 0 2 1 */
```

## Posición 3

La posición 3 contiene lo más importante que puede afectar su especificidad: el **id**.

Cada elemento puede tener un id asignado, y podemos usarlo en nuestra hoja de estilos para apuntar al elemento.

Ejemplos:

```css
#name {}       /* 0 1 0 0 */
.user #name {} /* 0 1 1 0 */
#name span {}  /* 0 1 0 1 */
```

## Posición 4

La posición 4 se ve afectada por los estilos en línea. Cualquier estilo en línea tendrá prioridad sobre cualquier regla definida en un archivo CSS externo o dentro de la etiqueta style en el encabezado de la página.

Ejemplos:

```html
<p style="color: red">Test</p> /* 1 0 0 0 */
```

Si alguna otra regla en el CSS define el color, esta regla de estilo en línea se aplicará de todas formas.  
Excepto por un caso, si se utiliza ```!important```

## !important

Agregar ```!important``` en una regla CSS hará que esa regla sea más importante que cualquier otra regla. 

```css
p {
font-size: 20px!important;
}
```

La única forma en que otra regla puede tener prioridad es tener ```!important``` también, y tener mayor especificidad en las otras posiciones.

## Herramientas para calcular la especificidad.

Puede usar el sitio https://specificity.keegan.st/ para realizar el cálculo de especificidad.  