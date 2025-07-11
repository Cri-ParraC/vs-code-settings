---
applyTo: "**/*.js,**/*.mjs"
---
Utilizar *template literals* para interpolar cadenas, en lugar de concatenaciones:

```js
// ✅ Correcto
console.log(`Hello ${name}`);

// ❌ Incorrecto
console.log("Hello " + name);
```

Para declarar variables, se tiene que usar `const` por defecto y `let` solo cuando sea necesario reasignarlas.

En sentencias condicionales, se deben evaluar expresiones booleanas explícitamente:

```js
// ✅ Correcto
if (isActive === true) {...}
if (isActive === false) {...}

// ❌ Incorrecto
if (isActive) {...}
if (!isActive) {...}
```

Para valores por defecto, se debe utilizar `??` y `??=`, en lugar de `||` y `||=`:

```js
// ✅ Correcto
const count = userCount ?? 0;
const message = inputText ?? "Sin texto";
config.timeout ??= 3000;

// ❌ Incorrecto
const count = userCount || 0;
const message = inputText || "Sin texto";
config.timeout ||= 3000;
```

Para acceder a propiedades anidadas, se debe usar `?.` y `??`:

```js
// ✅ Correcto
const firstName = user?.profile?.firstName ?? 'Unnamed';
```


## Comprobaciones de tipo explícitas

Para arreglos, se tiene que usar `Array.isArray(x)`:

```js
// ✅ Correcto
if (Array.isArray(arr)) {...}
```

Para tipos primitivos, se tiene que usar el operador `typeof`:

```js
// ✅ Correcto
if (typeof text === 'string') {...}
if (typeof count === 'number') {...}
if (typeof flag === 'boolean') {...}
...
```

Para `NaN`, se tiene que usar  `Number.isNaN()`:

```js
// ✅ Correcto
if (Number.isNaN(value)) {...}

// ❌ Incorrecto
if (isNaN(value)) {...}
```

Para valores *nullish* (`null` o `undefined`):

```js
// ✅ Correcto
if (value == null) {...}
if (value != null) {...}

// ❌ Incorrecto
if (value === null || value === undefined) {...}
if (value !== null || value !== undefined) {...}
```

## Nomenclatura de identificadores

**camelCase** para variables y funciones.

**PascalCase** para clases y componentes.

**UPPER_SNAKE_CASE** para constantes con valor primitivo inmutable.

## Formato de código

Punto y coma obligatorios.

2 espacios de indentación.

No abreviar los nombres de variables. Es preferible tener nombres largos y semánticos, que cortos e ilegibles.

```js
// ✅ Correcto
products.map((product) => product.value);

// ❌ Incorrecto
products.map((p) => p.value);
```

Para arreglos y objetos literales, se debe dejar *trailing comma*:

```js
// ✅ Correcto
const fruits = [
  'apple',
  'orange',
  'banana',
];
// ❌ Incorrecto
const fruits = [
  'apple',
  'orange',
  'banana'
];
```
```js
// ✅ Correcto
const person = {
  name: 'John',
  age: 30,
  city: 'New York',
};
// ❌ Incorrecto
const person = {
  name: 'John',
  age: 30,
  city: 'New York'
};
```

Para sentencias condicionales `if` de una sola linea, se pueden omitir las llaves, pero no se permite que la instrucción esté en la misma linea.

```js
// ✅ Correcto
if (isAdmin)
  showAdminPanel();

// ❌ Incorrecto
if (isAdmin) showAdminPanel();

// ❌ Incorrecto
if (isAdmin)
  showAdminPanel();
else
  showUserPanel();
```

Para funciones flecha, se debe usar paréntesis incluso para un único parámetro:

```js
// ✅ Correcto
items.map((item) => item.value);

// ❌ Incorrecto
items.map(item => item.value);
```

Preferir *guard clauses* en lugar de anidaciones profundas.

```js
// ✅ Correcto
function processOrder(order) {
  if (order == null) 
    return null;
  
  if (order.items == null) 
    return null;
  
  return calculateTotal(order.items);
}

// ❌ Incorrecto
function processOrder(order) {
  if (order != null) {
    if (order.items != null) {
      return calculateTotal(order.items);
    }
  }
  return null;
}
```

En los métodos de `array` que utilizan *callbacks* (como filter, map, find), al realizar comparaciones, el parámetro del *callback* debe aparecer primero en la expresión de comparación.

```js
// ✅ Correcto
users.find((user) => user.name === searchName);

// ❌ Incorrecto
users.find((user) => searchName === user.name);
```

Las variables booleanas deben nombrarse en positivo y usar prefijos como `is`, `has`, `can`, `should`.

```js
// ✅ Correcto
const isActive = true;
const hasPermission = checkPermissions();
const shouldRedirect = status === 404;

// ❌ Incorrecto
const active = true;
const permission = checkPermissions();
const redirect = status === 404;
```

El operador ternario debe usarse solo para asignaciones simples con una única condición.

```js
// ✅ Correcto
const status = isActive ? 'active' : 'inactive';

// ✅ Correcto
let message;
if (isAdmin) {
  message = userIsActive ? 'Admin active' : 'Admin inactive';
} else {
  message = isSpecialUser ? 'Special user' : 'Regular user';
}

// ❌ Incorrecto
const message = isAdmin
  ? userIsActive
    ? 'Admin is active'
    : 'Admin is inactive'
  : isSpecialUser
    ? 'Special user'
    : 'Regular user';
```

En funciones que retornan estructuras de datos complejas, es preferible guardar el objeto en una variable antes de retornarlo, para mejorar la legibilidad y facilitar la depuración.

```js
// ✅ Correcto
function getUser() {
  const user = { 
    name: 'John', 
    age: 30,
    permissions: ['read', 'write']
  };
  
  return user;
}

// ❌ Incorrecto
function getUser() {
  return { 
    name: 'John', 
    age: 30,
    permissions: ['read', 'write']
  };
}
```

## Documentación JSDoc

No es necesario dar una descripción de la función ni de cada parámetro.