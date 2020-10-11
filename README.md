# regexp
Ejemplos de expresiones regulares. Esto es una ayuda para quien tenga que construir una expresión regular  
y no sepa como hacerlo.  
Los ejemplos están desarrollados con el método test de regexp. El método "test" devuelve true cuando hay  
coincidencia del patrón dentro de la cadena analizada y false cuando no.  
Los ejemplos tienen la estructura:
 ```
 let patr = /patron/;  
 console.log (Descripción prueba, patr.test(cadena a analizar));
 ```
##  Ejemplos
```
// Expresión regular sencilla>
let patr = /abc/; // contiene la subcadena 'abc'
console.log ("Creación expresión: true", patr.test("abcdefghi"));
console.log ("Creación expresión: false", patr.test("acdefghi"));
```

```
// Caracteres: Letras, numeros, espacios, etc
patr = /[abc]/; // contiene a y/o b y/o c
console.log ("Caracteres 1: true", patr.test("acdefghi"));
patr = /[a-c]/; 
console.log ("Caracteres 2: true", patr.test("acdefghi"));
patr = /[abc]/; 
console.log ("Caracteres 3: false", patr.test("defghi"));
patr = /[a-zA-Z0-9]/; //contiene alguna minúscula, mayúscula y/o un número del 0 al 9
console.log ("Caracteres 4: true", patr.test("defghi Amarillo"));
console.log ("Caracteres 5: true", patr.test("defghi98-Amarillo"));
console.log ("Caracteres 6: false", patr.test("!$%&/()="));
patr = /[^0-9]/; //negación, no contiene solo números del 0 al 9
console.log ("Caracteres 7: true", patr.test("98 y otras cosas"));
console.log ("Caracteres 8: false", patr.test("98"));
```

```
// Meta-caracteres (Ver tablas de meta-caracteres en readme)
patr = /\s/; // contiene caracter no visible en print (tabulador, espacio, salto linea, enter, form feed)
console.log ("Meta-caracteres 1: true", patr.test("una   línea"));
patr = /\d/; // contiene dígitos del 0 al 9. Idéntico [0-9]
console.log ("Meta-caracteres 2: true", patr.test("Algo un numero 88"));
console.log ("Meta-caracteres 3: false", patr.test("Algo y no hay número"));
```

```
// Caracteres de comienzo y fin 
patr = /^auto$/; // contiene exactamente auto
console.log("Comienzo y fin 1: true", patr.test("auto"));
console.log("Comienzo y fin 2: false", patr.test("automático"));
console.log("Comienzo y fin 3: false", patr.test("Qué bonito auto"));

patr = /auto$/; // acaba en auto
console.log("Comienzo y fin 4: true", patr.test("Qué bonito es el auto"));
console.log("Comienzo y fin 5: false", patr.test("Qué bonito es el auto rojo"));
```

```
// Boundaries. Definen límites de palabra.
patr = /\bco/; // La palabra empieza por "co"
console.log('Ejemplo de boundary 1 true ', patr.test("coche"));
console.log('Ejemplo de boundary 2 true ', patr.test("iré en coche"));
console.log('Ejemplo de boundary 3 false ', patr.test("acometida"));
```

```
// Caracter "." indica cualquier caracter
patr = /.......uto/;  // 7 caracteres cualesquiera y las cadena uto a continuación
console.log('Cualquier caracter 1 false', patr.test("auto"));
console.log('Cualquier caracter 2 false', patr.test("automatic"));
console.log('Cualquier caracter 3 true', patr.test("distributor"));
```

```
// Operadores de repetición: +, * y ?
patr = /[a-f]+/; // contiene una a o varias, o una b, .. o una f
console.log('Operador + 1: true', patr.test("Hace 10 días que no le veo"));
console.log('Operador + 2: true', patr.test("castaña"));
console.log('Operador + 3: false', patr.test("Auto"));
console.log('Operador + 4: false', patr.test("42"));

patr = /[a-f]*/; // contiene ninguna a o varias, o ninguna b, .. o una f
console.log('Operador * 1: true', patr.test("Hace 10 días que no le veo"));
console.log('Operador * 2: true', patr.test("castaña"));
console.log('Operador * 3: true', patr.test("Auto"));
console.log('Operador * 4: true', patr.test("42"));

patr =/^a.*/; //comienza por a minúscula
console.log('Operador * 5: false', patr.test("amarillo"));
console.log('Operador * 5: false', patr.test("rojo"));

patr = /.a?../; // En la segunda posición hay una a o ninguna
console.log('Operador ? 1: true', patr.test("casa"));
console.log('Operador ? 2: true', patr.test("sal"));
console.log('Operador ? 3: true', patr.test("box"));
console.log('Operador ? 4: false', patr.test("42"));

patr = /.al{2}../; // hay a en la segunda y l se repite 2 veces en la tercera y cuarta posición 
console.log('Operador {num} 1: true', patr.test("sallgo"));
console.log('Operador {num} 2: false', patr.test("palo"));

patr = /.a{1,5}../; // desde la segunda posición a se repite de 1 a 5 veces
console.log('Operador {min,max} 1: false', patr.test("polo"));
console.log('Operador {min,max} 2: true', patr.test("vaale"));
console.log('Operador {min,max} 2: true', patr.test("vaaaaale"));
```

```
// Grupos
patr = /(ab)+/; // se repite la cadena 'ab' una vez o varias. Entre paréntesis se especifican grupos
console.log('Ejemplo de grupo 1: true ',patr.test("abc"));
console.log('Ejemplo de grupo 2: true ',patr.test("abcabc"));
console.log('Ejemplo de grupo 3: false',patr.test("aacbb"));
```

```
//Referencias
patr = /(ab)+...\1/; 
// se repite la cadena 'ab' una vez o varias después tres caracteres cualesquiera y finalmente 'ab' una o varias veces.
// \1 es una referencia al grupo 1, en este caso (ab).
console.log('Ejemplo de referencia 1: true ',patr.test("abcccab"));
console.log('Ejemplo de referencia 2: false ',patr.test("abccc"));
console.log('Ejemplo de referencia 3: true',patr.test("abacbab")); 
```

## Caracteres especiales en expresiones regulares

Caracter|Significado
---------|-----------
ˆ | Permite establecer como a de comenzar la cadena
$ | Permite establecer como termina la cadena
\* | Ninguno o cualquier número de caracteres
\+ | Uno o cualquier número de caracteres
\? | Ninguno o un caracte.
[] | Determina caracteres que puede contener la cadena.
() | Grupo de caracteres o cadenas.
{} | marcador de repetición
\ | marca caracteres especiales para que dejen de tener el significado especial. Caracter de escape.
. | representa un caracter.

## Metacaracteres abreviatura

Metacaracter|Significado
------------|-----------
\\t | 	Tabulador
\\n | 	Nueva línea
\\r | 	Retorno (carriage return)
\\f | 	Form feed
\\v | 	Tabulador vertical
\\s | 	Espacio (no visible en impresión, incluye \t, espacio, \n, \r, \f)
S | Negación de \s
\\w | Caracter alfanumérico
W |	La negación de \w 
\\d |	Dígitos [0-9] 
D |	Negación de \d 
\\b | Frontera de palabra
B |	Negación de \b 
\\0 | Nulo (nil) 
\\xxx | Caracter escrito en octal
\\xdd | Caracter escrito en hexadecimal
\\uxxxx | 	Caracter Unicode escrito en hexadecimal
\\cxxx |	Control, valor ASCII 

## Operadores de repetición

Operador|Significado|Descripción
--------|-----------|-----------
\? |	0 – 1 |	Ninguno o uno
\* |	0 – ∞ |	Ninguno o varios
\+ |	1 – ∞ |	Uno o varios
{num} | número | Exactamente número 
{min,} | min – ∞| Mínimo min 
{,max} |	0 – max	| Ninguno o un máximo de max
{min, max} | min – max	| Minimo min y máximo max 
