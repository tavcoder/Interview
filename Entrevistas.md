1. ¿Qué es un closure?

Un closure es una función que “recuerda” el alcance léxico en el que fue creada,
incluso después de que ese contexto haya terminado de ejecutarse. Una closure es la combinación de una función con el entorno lexico en el cual se declara dicha función. La palabra lexico hace referencia al hecho de que el contexto lexico referencia donde se declara una variable dentro del código para determinar que parte del código puede acceder a dicha variable. Una closure es una función que tiene acceso a las variables declaradas en el contexto externo aún cuando la función externa ya haya finalizado su ejecución.
Porque utilizaría una?

Emular metodos privados con closures. Comunmente usada en el patron modulo.
2. Promises
Un Promise es un objeto que representa la eventual finalización (o falla) de una operación asíncrona y su valor resultante.
Estados de un promise:
pending (pendiente)
fulfilled (resuelta)
rejected (rechazada)
Permite encadenar múltiples operaciones con .then() y manejar errores con .catch().
3. Diferencia entre Promise y Callback
| Característica    | Callback                               | Promise                            |
| ----------------- | -------------------------------------- | ---------------------------------- |
| Encadenamiento    | Difícil, puede generar “callback hell” | Fácil con `.then()`                |
| Manejo de errores | Cada callback maneja su error          | `.catch()` centralizado            |
| Valor resultante  | Pasado a la función callback           | Resuelto con `resolve`             |
| Estado            | No hay estado definido                 | `pending`, `fulfilled`, `rejected` |
1. CSS Box Model

Cada elemento HTML se compone de cuatro capas:
+-------------------------+
|       Margin            | <- espacio fuera del borde
+-------------------------+
|       Border            | <- borde del elemento
+-------------------------+
|       Padding           | <- espacio interno entre contenido y borde
+-------------------------+
|       Content           | <- contenido real (texto, imagen, etc.)
+-------------------------+
width y height afectan solo el content por defecto.
Para incluir padding y border dentro del ancho total: box-sizing: border-box;
2. CSS Position
Propiedades de posición y diferencias:
| Position   | Descripción                                                                                     |
| ---------- | ----------------------------------------------------------------------------------------------- |
| `static`   | Por defecto; sigue el flujo normal del documento.                                               |
| `relative` | Relativo a su posición original; se mueve con `top`, `left`, etc.                               |
| `absolute` | Relativo al **primer padre posicionado** (no estático); sale del flujo normal                   |
| `fixed`    | Fijo respecto a la ventana; no se mueve al hacer scroll                                         |
| `sticky`   | Se comporta como `relative` hasta que se alcanza un punto de scroll, luego se fija como `fixed` |
3. Delegación de eventos
La delegación de eventos es una técnica de JavaScript donde se asigna un escuchador (listener) a un elemento padre en lugar de a cada hijo.
Cuando ocurre un evento en un hijo, este “sube” (propagación o bubbling) hasta el padre, que puede capturarlo y actuar según sea necesario.
Beneficios
Menor uso de memoria
Solo necesitas un listener en el padre, en lugar de uno en cada hijo.
No hay que manejar dinámicamente elementos
Si se eliminan o agregan hijos, no necesitas quitar ni agregar listeners.
| **Forma de llamada / Regla**                | **Descripción de `this`**                                                                                                          | **Ejemplo con `this`**                                                                                        |
| ------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **Invocación con `new`**                    | `this` apunta a un nuevo objeto vacío creado por la función.                                                                       | `function Persona() { this.nombre = "Ana"; } const p = new Persona(); console.log(p.nombre); // Ana`          |
| **Invocación con `call`, `apply` o `bind`** | `this` será el objeto que se pase como argumento a `call`, `apply` o `bind`.                                                       | `function saludar() { console.log(this.nombre); } const obj = { nombre: "Luis" }; saludar.call(obj); // Luis` |
| **Método de un objeto (`obj.method()`)**    | `this` es el objeto que contiene la función como propiedad.                                                                        | `const obj = { nombre: "Marta", decir: function() { console.log(this.nombre); } }; obj.decir(); // Marta`     |
| **Función invocada de forma regular**       | `this` apunta al objeto global (`window` en navegador). En modo estricto, `this` es `undefined`.                                   | `function mostrar() { console.log(this); } mostrar(); // window (o undefined en strict mode)`                 |
| **Prioridad de reglas**                     | Si varias reglas aplican, la regla de mayor prioridad prevalece: `new` > `call/apply/bind` > método de objeto > invocación normal. | N/A                                                                                                           |
| **Funciones flecha (ES6)**                  | `this` **ignora todas las reglas anteriores** y toma el valor del contexto donde se creó la función.                               | `const obj = { nombre: "Ana", flecha: () => console.log(this.nombre) }; obj.flecha(); // undefined`           |
Explique como funciona la herencia de prototipos
Esta es una pregunta muy común en las entrevistas de Javascript. Todos lo objetos de Javascript tienen una propiedad __proto__ que referencia a otro objetos, el cual se llama el prototipo del objeto. Cuando se accede a una propiedad de un objeto, se busca si el objeto tiene esa propiedad, si no la tiene, el engine de Javascript buscara en el objeto referenciado por __proto__ y si este no tuviese la propiedad, seguira buscando por la cadena de prototipos hasta encontrar la propiedad o hasta llegar al final de la cadena de prototipo. Esto simula la herencia clasica de objetos, pero es más bien una delegación que herencia.
Explique la diferencia cuando una variable es: null, undefined o undeclared. Como chequearia cada uno de estos estados?
Las variables no declaradas son una mala páctica, de la misma forma que las variables globales son una mala práctica.
Como recomendación personal, nunca dejar las variables no declaradas o no asignadas, sino que es conveniente asignarle explicitamente el valor null al momento de declarar la variable si no tiene un valor especifico aún. Si se utiliza algún tipo de linter, se pueden crear reglas para verificar que no se haga referencia a variables no declaradas.
| **Tipo de variable**          | **Descripción**                                                                                                                                                        | **Cómo chequearlo**                                          | **Notas**                                                         |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ | ----------------------------------------------------------------- |
| **Undeclared** (no declarada) | Variable **no creada previamente** con `var`, `let` o `const`. Si se asigna fuera de contexto estricto, se crea como global. En modo estricto, lanza `ReferenceError`. | Intentar accederla lanzará un error.                         | Mala práctica; evita crear variables sin declarar.                |
| **Undefined**                 | Variable **declarada pero sin valor asignado**. También es el valor por defecto que devuelve una función sin `return`.                                                 | `variable === undefined` o `typeof variable === 'undefined'` | No usar `== undefined` porque también devuelve true para `null`.  |
| **Null**                      | Variable a la que se le ha asignado **explícitamente** el valor `null`.                                                                                                | `variable === null`                                          | No usar `== null` porque también devolverá true para `undefined`. |
What is CSS selector specificity and how does it work?
“Mantén baja especificidad para facilitar sobrescribir reglas”
En CSS, la especificidad determina qué regla gana cuando varias coinciden en un mismo elemento.
Alta especificidad: selectores con muchos IDs, clases y elementos combinados o estilos inline (a=1, b>0).
Baja especificidad: selectores simples, como solo un tag (div) o solo una clase (.btn).
What's the difference between "resetting" and "normalizing" CSS? Which would you choose, and why?
I would choose resetting when I have a very customized or unconventional site design such that I need to do a lot of my own styling and do not need any default styling to be preserved.
| Característica          | Resetting                             | Normalizing                                                         |
| ----------------------- | ------------------------------------- | ------------------------------------------------------------------- |
| Qué hace                | Elimina todos los estilos por defecto | Mantiene estilos útiles y corrige inconsistencias entre navegadores |
| Necesidad de redeclarar | Alta                                  | Baja                                                                |
| Control sobre estilos   | Total                                 | Parcial                                                             |
| Uso típico              | Empezar desde cero                    | Lograr consistencia cross-browser                                   |
Describe floats and how they work

Ejemplo: 0,1,0,0 > 0,0,10,10 porque el ID tiene mayor prioridad que clases o tags.
Describe floats and how they work.(no lo entiendo)
| Concepto          | Qué hace / Uso                                                                  |
| ----------------- | ------------------------------------------------------------------------------- |
| `float`           | Flota elementos a izquierda o derecha, texto/flujos alrededor                   |
| `clear`           | Detiene el flujo alrededor de flotados, se usa para posicionar elementos debajo |
| Problema altura   | Contenedor solo con flotados colapsa a altura 0                                 |
| Solución clearfix | Pseudo-elemento `::after` con `clear: both` para expandir contenedor            |
| Solución overflow | `overflow: auto/hidden` crea block formatting context y expande el contenedor   |
Describe z-index and how stacking context is formed.
 only certain elements create stacking contexts. Elements that don't create their own stacking contexts are assimilated by the parent stacking context.
 | Concepto            | Explicación breve                                                  |
| ------------------- | ------------------------------------------------------------------ |
| `z-index`           | Controla el orden de apilamiento en el eje Z                       |
| Requisito           | Solo funciona si `position` ≠ `static`                             |
| Sin `z-index`       | Se apilan según el orden en el DOM                                 |
| *Stacking context*  | Grupo aislado de capas; los hijos no pueden sobrepasar sus límites |
| Cómo se crea        | `position` + `z-index`, `opacity<1`, `transform`, `filter`, etc.   |
| Importante recordar | Cada stacking context es independiente del resto                   |
Describe Block Formatting Context (BFC) and how it works
