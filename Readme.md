Cashify 💸
Biblioteca de conversión de moneda ligera, sucesora de money.js

Estado de construcción Estado de cobertura Estilo de código XO instalar tamaño tamaño minificado Mencionado en Awesome Node.js

Motivación
Destacar
Instalar en pc
Uso
Con constructor
Sin constructor
Analizando
Integración con currency.js
API
Cashify ({base, rates})
base
tarifas
convertir (cantidad, {desde, hasta, base, tarifas})
cantidad
de
a
base
tarifas
parse (expresión)
expresión
Migrar desde money.js
Problemas de punto flotante
Proyectos relacionados
Licencia
Motivación
Este paquete se creó porque la popular biblioteca money.js :

no se mantiene (la última confirmación fue hace ~ 5 años)
tiene más de 20 problemas abiertos
no es compatible con TypeScript
tiene globales implícitas
no tiene pruebas unitarias
tiene problemas de punto flotante
Destacar
API simple
0 dependencias
Mantenido activamente
Bien probado
Fácil migración desde money.js
Escrito en TypeScript
Instalar en pc
$ npm install cashify
Uso
Con constructor
const  { Cashify }  =  require ( 'cashify' ) ;

 tasas  constantes =  { 
	GBP : 0.92 , 
	EUR : 1.00 , 
	USD : 1.12 
} ;

const  cashify  =  new  Cashify ( { base : 'EUR' , tarifas } ) ;

 resultado  constante =  cobrar . convertir ( 10 ,  { de : 'EUR' ,  a : 'GBP' } ) ;

consola . log ( resultado ) ;  // => 9.2
Sin constructor
CashifyNo es necesario utilizar el constructor. En su lugar, puede usar la convertfunción:

const  { convertir }  =  require ( 'cobrar' ) ;

 tasas  constantes =  { 
	GBP : 0.92 , 
	EUR : 1.00 , 
	USD : 1.12 
} ;

 resultado  constante =  convertir ( 10 ,  { de : 'EUR' ,  a : 'GBP' ,  base : 'EUR' , tarifas } ) ;

consola . log ( resultado ) ;  // => 9.2
Analizando
Cashify admite el análisis, por lo que puede pasar un stringal amountargumento y la moneda fromy / o la tomoneda se detectarán automáticamente:

const  { Cashify }  =  require ( 'cashify' ) ;

 tasas  constantes =  { 
	GBP : 0.92 , 
	EUR : 1.00 , 
	USD : 1.12 
} ;

const  cashify  =  new  Cashify ( { base : 'EUR' , tarifas } ) ;

// 
Cashify de análisis básico . convertir ( '€ 10 EUR' ,  { a : 'GBP' } ) ;

// 
Cashify de análisis completo . convertir ( '10 EUR a GBP ' ) ;
Alternativamente, si solo desea analizar un stringsin conversión, puede usar la parsefunción, que devuelve un objectcon los resultados del análisis:

const  { analizar }  =  require ( 'cobrar' ) ;

analizar ( '10 EUR a GBP ' ) ;  // => {monto: 10, desde: 'EUR', hasta: 'GBP'}
Nota: Si desea utilizar el análisis completo, debe pasar un stringformato específico:

10 usd to pln
12.5 GBP in EUR
3.1415 eur as chf
Puede usar to, ino aspara separar la expresión (no distingue entre mayúsculas y minúsculas). Las mayúsculas y minúsculas de las monedas usadas no importa, ya que Cashify las convertirá automáticamente a mayúsculas.


Integración con currency.js
currency.js es una biblioteca pequeña y liviana para trabajar con valores de moneda. Funciona muy bien con Cashify. En el siguiente ejemplo lo estamos usando para formatear el resultado de la conversión:

const  { Cashify }  =  require ( 'cashify' ) ; 
const  moneda  =  require ( 'moneda.js' ) ;

 tasas  constantes =  { 
	GBP : 0.92 , 
	EUR : 1.00 , 
	USD : 1.12 
} ;

const  cashify  =  new  Cashify ( { base : 'EUR' , tarifas } ) ;

const  convertido  =  cobrar . convertir ( 8635619 ,  { de : 'EUR' ,  a : 'GBP' } ) ;  // => 7944769.48

// Formatea la 
moneda del resultado de la conversión ( convertida ,  { símbolo : '€' ,  formatWithSymbol : true } ) . formato ( ) ;  // => 7944769,48 €
API
Cashify ({base, rates})
Constructor

base
Tipo: string

Moneda base

tarifas
Tipo: object

Objeto que contiene tipos de cambio (por ejemplo, de una API, como tipos de cambio abiertos)

convertir (cantidad, {desde, hasta, base, tarifas}) with and without constructor
Devuelve el resultado de la conversión ( number)

cantidad
Tipo: numberostring

Cantidad de dinero que desea convertir. Puede utilizar a numbero a string. Si elige la segunda opción, puede aprovechar el análisis y no especificar fromy / o toargumento (s).

de
Tipo: string

Moneda desde la que desea convertir. Es posible que no necesite especificarlo si está utilizando el análisis .

a
Tipo: string

Moneda a la que desea convertir. Es posible que no necesite especificarlo si está utilizando el análisis .

base
Tipo: string

Moneda base

tarifas
Tipo: object

Objeto que contiene tipos de cambio (por ejemplo, de una API, como tipos de cambio abiertos)

parse (expresión)
Devuelve un object, que contiene los resultados del análisis:

{
	amount: number;
	from: string | undefined;
	to: string | undefined;
}
expresión
Tipo: string

Expresión que desea analizar, ej. 10 usd to plno€1.23 eur

Migrar desde money.js
Con Cashifyconstructor:

- const fx = require ('dinero'); 
+ const {Cashify} = require ('cobrar');

- fx.base = 'EUR'; 
- fx.rates = { 
- 	GBP: 0,92, 
- 	EUR: 1,00, 
- 	USD: 1,12 
- };

+ tasas constantes = { 
+ 	 GBP: 0.92, 
+ 	 EUR: 1.00, 
+ 	 USD: 1.12 
+ };

+ const cashify = new Cashify ({base: 'EUR', tarifas});

- fx.convert (10, {desde: 'GBP' hasta: 'EUR'}); 
+ cashify.convert (10, {de: 'GBP', a: 'EUR'});
Con convertfunción:

- const fx = require ('dinero'); 
+ const {convertir} = requerir ('cobrar');

- fx.base = 'EUR'; 
- fx.rates = { 
- 	GBP: 0,92, 
- 	EUR: 1,00, 
- 	USD: 1,12 
- };

+ tasas constantes = { 
+ 	 GBP: 0.92, 
+ 	 EUR: 1.00, 
+ 	 USD: 1.12 
+ };

- fx.convert (10, {desde: 'GBP' hasta: 'EUR'}); 
+ convertir (10, {de: 'GBP', a: 'EUR', base: 'EUR', tarifas});
Problemas de punto flotante
Cuando se trabaja con monedas, los decimales solo deben ser precisos hasta el valor de centavo más pequeño y, al mismo tiempo, evitar errores comunes de coma flotante al realizar operaciones aritméticas básicas.

Echemos un vistazo al siguiente ejemplo:

const  fx  =  require ( 'dinero' ) ; 
const  { Cashify }  =  require ( 'cashify' ) ;

 tasas  constantes =  { 
	GBP : 0.92 , 
	USD : 1.12 
} ;

fx . tarifas  =  tarifas ; 
fx . base  =  'EUR' ;

const  cashify  =  new  Cashify ( { base : 'EUR' , tarifas } ) ;

fx . convertir ( 10 ,  { de : 'EUR' ,  a : 'GBP' } ) ;  // => 9.200000000000001 
cobrar . convertir ( 10 ,  { de : 'EUR' ,  a : 'GBP' } ) ;  // => 9.2
Como puede ver, money.js no maneja las monedas correctamente y, por lo tanto, se están produciendo problemas de punto flotante. Aunque solo hay una pequeña discrepancia entre los resultados, si está convirtiendo grandes cantidades, eso puede sumarse.

Cashify resuelve este problema de la misma manera que currency.js , trabajando con números enteros entre bastidores. Esto debería estar bien para la mayoría de los valores razonables de monedas.

Proyectos relacionados
currency.js : biblioteca javascript ligera para trabajar con valores de moneda.
cashify-rs - Puerto de Cashify para Rust.
Licencia
MIT © Antoni Kepinski
