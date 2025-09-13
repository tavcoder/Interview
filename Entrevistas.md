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

4. Diferencia entre Promise y Callback
   
| Característica    | Callback                               | Promise                            |
| ----------------- | -------------------------------------- | ---------------------------------- |
| Encadenamiento    | Difícil, puede generar “callback hell” | Fácil con `.then()`                |
| Manejo de errores | Cada callback maneja su error          | `.catch()` centralizado            |
| Valor resultante  | Pasado a la función callback           | Resuelto con `resolve`             |
| Estado            | No hay estado definido                 | `pending`, `fulfilled`, `rejected` |

Explique la delegación de eventos

| Concepto                  | Descripción                 | Beneficios      
| Función                                                 | Propósito | Cómo funciona             | Ejemplo de uso                | Se detiene con  
| **`setTimeout(fn, delay)`**                                   | Ejecutar una función **una vez** después de un tiempo específico.                         | Llama a `fn` después de `delay` ms.                                                                                            | `js setTimeout(() => { console.log('Hola después de 2s'); }, 2000); `                                                                                               | `clearTimeout(id)`                                           |
| **`setInterval(fn, delay)`**                                  | Ejecutar una función **repetidamente** cada intervalo de tiempo.                          | Llama a `fn` cada `delay` ms hasta que se detenga.                                                                             | `js const id = setInterval(() => { console.log('Esto se repite cada 1s'); }, 1000); `                                                                               | `clearInterval(id)`                                          |
| **`debounce(fn, delay)`** *(no nativo, se implementa con JS)* | Ejecutar una función **una sola vez** después de que deje de activarse por cierto tiempo. | Reinicia el temporizador cada vez que el evento se dispara. `fn` solo se ejecuta cuando ha pasado `delay` ms sin más disparos. | `js const input = document.querySelector('input'); const debounced = debounce(() => { console.log('Buscar'); }, 300); input.addEventListener('input', debounced); ` | Cancelando el timeout interno                                |
| **`throttle(fn, delay)`** *(no nativo, se implementa con JS)* | Limitar la ejecución de una función a **una vez cada intervalo de tiempo**.               | Garantiza que `fn` se ejecute como máximo una vez cada `delay` ms, aunque el evento se dispare muchas veces.                   | `js window.addEventListener('scroll', throttle(() => { console.log('Scroll limitado a 200ms'); }, 200)); `                                            | Dependiendo de la implementación, limpiar el timeout interno |

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

3. CSS Position
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
A BFC is an HTML box that satisfies at least one of the following | Concepto                  | Descripción breve                                                                  |
| ------------------------- | ---------------------------------------------------------------------------------- |
| Qué es                    | Zona de renderizado aislada para elementos de tipo bloque                          |
| Qué hace                  | Aísla el contenido interno del contenido externo                                   |
| Cuándo se crea            | `float≠none`, `position=absolute/fixed`, `display` especial, `overflow≠visible`    |
| Efectos principales       | Contiene elementos flotados, evita colapso de altura, controla colapso de márgenes |
| Alineación dentro del BFC | Borde izquierdo (o derecho en RTL) del contenedor                                  |
What are the various clearing techniques and which is appropriate for what context?
In large projects, I would write a utility .clearfix class and use them in places where I need it. overflow: hidden might clip children if the children is taller than the parent and is not very ideal.
| Qué es                              | Cómo se crea                                                                            | Por qué es útil                            
| Contexto aislado de cajas en bloque | float≠none, position≠static/relative, display: inline-block/flex/grid, overflow≠visible | Contiene flotados y evita colapso de altura/márgenes |
Qué pasa cuando usas float en elementos hijos
Cuando aplicas float a un elemento (por ejemplo float: left;), ese elemento sale del flujo normal del documento.
Al estar “fuera del flujo”, su contenedor ya no lo tiene en cuenta para calcular su altura.
Como resultado, el contenedor colapsa: su altura se vuelve 0, como si no tuviera contenido.
📌 Ejemplo visual mental:
Tienes un contenedor <div> y dentro pones dos cajas flotantes.
Las cajas flotantes se ven en pantalla, pero el contenedor parece "desaparecer" porque no envuelve a esas cajas.
🛠 Por qué hay que "limpiar" (clear)
Para que el contenedor reconozca de nuevo a sus hijos flotantes, debemos "limpiar" los floats.
Al limpiar, el contenedor vuelve a ajustar su altura al contenido interno.
Explain CSS sprites, and how you would implement them on a page or site.
CSS sprites combine multiple images into one single larger image. It is a commonly-used technique for icons (Gmail uses it). How to implement it:

Use a sprite generator that packs multiple images into one and generate the appropriate CSS for it.
Each image would have a corresponding CSS class with background-image, background-position and background-size properties defined.
To use that image, add the corresponding class to your element.
| Técnica     | Ventajas                                                  | Desventajas                                                     | Cuándo usarla                  
| CSS Sprites | Reduce solicitudes HTTP, carga anticipada evita parpadeos | Difícil de mantener, no escalable, requiere background-position | Muchos iconos pequeños y estáticos, proyectos sin HTTP/2                  |
| SVG         | Escalables, personalizables, buen soporte                 | Puede requerir optimización, complejo con muchos archivos       | Interfaces modernas, responsivas, cambiar color/tamaño fácilmente         |
| Icon Fonts  | Fácil de usar con pseudo-elementos, solo una solicitud    | Baja calidad en Retina, problemas de accesibilidad              | Interfaces simples, pocos iconos, compatibilidad con navegadores antiguos |
How would you approach fixing browser-specific styling issues?
After identifying the issue and the offending browser, use a separate style sheet that only loads when that specific browser is being used. This technique requires server-side rendering though.
Use libraries like Bootstrap that already handles these styling issues for you.
Use autoprefixer to automatically add vendor prefixes to your code.
Use Reset CSS or Normalize.css.
If you're using Postcss (or a similar transpiling library), there may be plugins which allow you to opt in for using modern CSS syntax (and even W3C proposals) that will transform those sections of your code into corresponding safe code that will work in the targets you've used.
How do you serve your pages for feature-constrained browsers? What techniques/processes do you use?
Graceful degradation - The practice of building an application for modern browsers while ensuring it remains functional in older browsers.
Progressive enhancement - The practice of building an application for a base level of user experience, but adding functional enhancements when a browser supports it.
Use caniuse.com to check for feature support.
Autoprefixer for automatic vendor prefix insertion.
Feature detection using Modernizr.
Use CSS Feature queries @support
| Técnica / Proceso                          | Qué es / Cómo funciona                                                                                                                       | Cuándo usarlo                                                                                                        |
| ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| **Graceful Degradation**                   | Se construye la aplicación para navegadores modernos y luego se asegura que funcione de forma básica en navegadores antiguos                 | Cuando tu público usa mayormente navegadores nuevos, pero necesitas soporte mínimo para antiguos                     |
| **Progressive Enhancement**                | Se construye una base funcional que funciona en todos los navegadores, y luego se agregan mejoras que solo funcionan en navegadores modernos | Ideal cuando quieres garantizar funcionalidad básica a todos los usuarios y mejorar la experiencia donde sea posible |
| **Feature Detection (Modernizr)**          | Detecta si el navegador soporta ciertas funcionalidades antes de usarlas                                                                     | Evitar errores y aplicar mejoras solo cuando el navegador las soporte                                                |
| **CSS Feature Queries (`@supports`)**      | Permite aplicar estilos solo si el navegador soporta cierta propiedad CSS                                                                    | Aplicar estilos avanzados solo donde se puedan renderizar correctamente                                              |
| **Autoprefixer**                           | Inserta automáticamente prefijos de proveedor (vendor prefixes) en CSS                                                                       | Ahorrar tiempo y garantizar compatibilidad con navegadores que requieren prefijos                                    |
| **Comprobar compatibilidad (caniuse.com)** | Verificar si un navegador soporta una propiedad o API antes de usarla                                                                        | Planificación y desarrollo de funcionalidades modernas con seguridad                                                 |
What are the different ways to visually hide content (and make it available only for screen readers)?
Even if WAI-ARIA is the ideal solution, I would go with the absolute positioning approach, as it has the least caveats, works for most elements and it's an easy technique.
| Situación                                            | Técnica recomendada                             | Por qué                                                                                                                                   |
| ---------------------------------------------------- | ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| **Botones o enlaces solo para lectores de pantalla** | `position: absolute; left: -99999px;`           | Quieres que exista un botón o link que haga algo útil para usuarios con lectores de pantalla, pero que no aparezca en la interfaz visual. |
| **Textos descriptivos que no deben ocupar espacio**  | `width: 0; height: 0;`                          | Por ejemplo, instrucciones adicionales o etiquetas que explican algo, solo accesibles para lectores de pantalla.                          |
| **Ocultar texto mientras se mantiene SEO**           | Meta tags / JSON-LD / Schema.org                | Información estructurada que no se muestra pero los motores de búsqueda o lectores de pantalla pueden usarla.                             |
| **Indicaciones adicionales dentro de un formulario** | WAI-ARIA (ej. `aria-label`, `aria-describedby`) | Etiquetas o instrucciones que no deben saturar la interfaz visual pero sí ser leídas por screen readers.                                  |
| **Decoración visual con texto**                      | `text-indent: -9999px`                          | Cuando quieres usar texto como parte de un diseño (por ejemplo, un logo de texto) pero visualmente reemplazado por un icono.              |
Have you ever used a grid system, and if so, what do you prefer?
| Sistema              | Descripción                                                     | Pros                                                                                | Contras                                                                         | Preferencia actual                                               |
| -------------------- | --------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| **Float-based grid** | Usaba `float` para colocar columnas lado a lado                 | Muy compatible con navegadores antiguos                                             | Difícil de mantener, necesita clearfix y hacks                                  | Obsoleto, solo para soporte legacy                               |
| **Flexbox**          | Usaba `display: flex` para crear filas y columnas flexibles     | Fácil de alinear elementos, más intuitivo que float, buena compatibilidad           | No tan potente para layouts complejos de varias dimensiones                     | Sistema recomendado actualmente para grids simples y responsivos |
| **CSS Grid Layout**  | Usa `display: grid` y propiedades de grid para filas y columnas | Permite layouts complejos en dos dimensiones (fila y columna), más control que Flex | Menor compatibilidad en navegadores muy antiguos, curva de aprendizaje más alta | Futuro estándar para grids, ideal para layouts avanzados         |
Have you used or implemented media queries or mobile-specific layouts/CSS?
Yes. An example would be transforming a stacked pill navigation into a fixed-bottom tab navigation beyond a certain breakpoint.
Are you familiar with styling SVG?
| Situación                      | Por qué modificarías el SVG                                                                             | Cómo lo harías                                                                                   |
| ------------------------------ | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| **Cambio de color según tema** | Por ejemplo, tu app tiene modo oscuro y claro y quieres que los íconos cambien de color automáticamente | Usando CSS (`fill`/`stroke`) sobre SVG inline o con clases                                       |
| **Animaciones**                | Hacer que partes del SVG se muevan, parpadeen o cambien de forma                                        | CSS animations, transitions o JavaScript manipulando atributos (`transform`, `stroke-dasharray`) |
| **Interactividad**             | Cambiar el color de un ícono al pasar el mouse o al hacer clic                                          | Pseudo-clases CSS (`:hover`, `:active`) o JS                                                     |
| **Personalización de iconos**  | Mostrar un logo con colores específicos según el usuario o sección de la web                            | Modificar `fill`/`stroke` dinámicamente con CSS o JS                                             |
| **Responsive design**          | Ajustar tamaño o posición del SVG según la pantalla                                                     | Usando `viewBox`, `width`, `height` y media queries                                              |
Can you give an example of an @media property other than screen?
Yes, there are four types of @media properties (including screen):

all - for all media type devices
print - for printers
speech - for screenreaders that "reads" the page out loud
screen - for computer screens, tablets, smart-phones etc.
What are some of the "gotchas" for writing efficient CSS?
| Concepto                                    | Qué significa                                                                                           | Consejos prácticos                                                        
| **Selector efficiency**                     | Los navegadores leen los selectores de **derecha a izquierda** (desde el key selector hacia los padres) | Evita selectores universales (`*`) y selectores de etiqueta (`div`, `p`) largos, ya que el navegador tiene que revisar muchos elementos  |
| **Longitud de selector**                    | Selectores muy largos o anidados hacen que el navegador tenga que recorrer más nodos                    | Usa **clases únicas**, nombres claros y evita anidamientos innecesarios                                                                  |
| **BEM (Block Element Modifier)**            | Metodología que usa clases únicas y jerarquía en el nombre                                              | Hace los selectores más simples y fáciles de sobreescribir sin afectar performance                                                       |
| **Propiedades que disparan reflow/repaint** | Algunas propiedades CSS hacen que el navegador recalculen el layout o repinten la página                | Evita cambiar `width`, `height`, `margin`, `padding` frecuentemente. Prefiere transformaciones (`transform`, `opacity`) para animaciones |
| **Reflow vs Repaint vs Compositing**        | Reflow: recalcula layout; Repaint: repinta elementos visuales; Compositing: GPU render                  | Optimiza animaciones usando propiedades que no disparen reflow (ej. `transform`, `opacity`)                                              |
What are the advantages/disadvantages of using CSS preprocessors?
| Categoría                      | Ventajas                                                                                  | Desventajas              
| **Mantenibilidad**             | Código más fácil de mantener y organizar                                                  | Requiere herramientas de compilación (preprocesamiento)                                       |
| **Selectores y anidamiento**   | Permite escribir selectores anidados de forma más clara                                   | Tiempo de recompilación puede ser lento en proyectos grandes                                  |
| **Variables / Theming**        | Variables para colores, tamaños y temas consistentes; se pueden compartir entre proyectos | Aprendes una sintaxis nueva que no es CSS nativo (aunque futuro CSS podría soportarlo)        |
| **Mixins y funciones**         | Reutilización de CSS repetido y configuración con loops, listas y mapas                   | Dependencia de la herramienta, no puedes usar directamente en producción sin compilar         |
| **Modularidad**                | Permite dividir código en múltiples archivos y luego compilar en uno solo                 | CSS nativo también se puede dividir, pero necesitaría múltiples requests si no se combina     |
| **Integración con Node/JS**    | Menos CSS escrito en JavaScript, compatible con Node                                      | Algunas implementaciones como node-sass requieren recompilación al cambiar de versión de Node |
| **Sintaxis propia (ej. Less)** | Variables con `@` fáciles de identificar                                                  | Puede confundirse con reglas nativas de CSS (`@media`, `@import`)     
|
Explain how a browser determines what elements match a CSS selector.
This part is related to the above about writing efficient CSS. Browsers match selectors from rightmost (key selector) to left. Browsers filter out elements in the DOM according to the key selector and traverse up its parent elements to determine matches. The shorter the length of the selector chain, the faster the browser can determine if that element matches the selector.
For example with this selector p span, browsers firstly find all the <span> elements and traverse up its parent all the way up to the root to find the <p> element. For a particular <span>, as soon as it finds a <p>, it knows that the <span> matches and can stop its matching.
Describe pseudo-elements and discuss what they are used for.
| Pseudo-elemento             | Qué hace                                                | Uso común / Ejemplo                                            |
| --------------------------- | ------------------------------------------------------- | -------------------------------------------------------------- |
| **::before**                | Inserta contenido antes del contenido del elemento      | Crear decoraciones, iconos, triángulos en tooltips, clearfix   |
| **::after**                 | Inserta contenido después del contenido del elemento    | Decoraciones, clearfix, efectos visuales sin modificar el HTML |
| **::first-line**            | Aplica estilos solo a la primera línea del texto        | Tipografía destacada, estilo de párrafo inicial                |
| **::first-letter**          | Aplica estilos solo a la primera letra del texto        | Letras capitales, decoraciones iniciales                       |
| **Otros (ej: ::selection)** | Permite estilizar otras partes específicas del elemento | Cambiar color de selección de texto, etc.                      |
Los pseudo-elementos permiten añadir contenido visual o decorativo sin tocar el HTML.
Fomentan la separación de responsabilidades: el HTML se mantiene semántico y el CSS maneja el estilo y decoración.
Explain your understanding of the box model and how you would tell the browser in CSS to render your layout in different box models.
The CSS box model describes the rectangular boxes that are generated for elements in the document tree and laid out according to the visual formatting model. Each box has a content area (e.g. text, an image, etc.) and optional surrounding padding, border, and margin areas.
| Modelo de caja                | Cómo funciona                                                                              | CSS                        |
| ----------------------------- | ------------------------------------------------------------------------------------------ | -------------------------- |
| **content-box (por defecto)** | `width` y `height` solo aplican al contenido. Padding y border se suman al tamaño total    | `box-sizing: content-box;` |
| **border-box**                | `width` y `height` incluyen contenido + padding + border. Hace más fácil controlar tamaños | `box-sizing: border-box;`  |
En layouts modernos, border-box es recomendado porque hace que el tamaño del elemento no cambie al agregar padding o border.
What does * { box-sizing: border-box; } do? What are its advantages?
By default, elements have box-sizing: content-box applied, and only the content size is being accounted for.
Taking into account paddings and borders as part of our box model resonates better with how designers actually imagine content in grids.
What is the CSS display property and can you give a few examples of its use?
| Valor            | Descripción                        | Comportamiento    
| **none**         | Oculta el elemento                 | El elemento **no se muestra** y no ocupa espacio; sus hijos tampoco se muestran |
| **block**        | Elemento de bloque                 | Ocupa toda la línea horizontal; empieza en nueva línea                          |
| **inline**       | Elemento en línea                  | Se coloca junto a otros elementos; no puedes asignarle width/height             |
| **inline-block** | Combinación inline + block         | Se comporta como inline pero permite width y height                             |
| **flex**         | Contenedor flexible                | Permite alinear y distribuir elementos hijos fácilmente usando flexbox          |
| **grid**         | Contenedor de cuadrícula           | Permite organizar hijos en filas y columnas usando CSS Grid                     |
| **table**        | Comportamiento similar a `<table>` | Útil para layouts de tipo tabla sin usar HTML `<table>`                         |
| **table-row**    | Comportamiento similar a `<tr>`    | Se usa dentro de `display: table` para definir filas                            |
| **table-cell**   | Comportamiento similar a `<td>`    | Se usa dentro de `display: table-row` para definir celdas                       |
| **list-item**    | Comportamiento similar a `<li>`    | Permite definir viñetas, numeración y estilos de lista     
display: none no es lo mismo que visibility: hidden, ya que este último deja el espacio ocupado.
inline-block es útil para botones o íconos que deben alinearse horizontalmente pero permitir width/height.
What's the difference between inline and inline-block?
| Característica                             | block                                                                  | inline-block                                         | inline                                                                     |
| ------------------------------------------ | ---------------------------------------------------------------------- | ---------------------------------------------------- | -------------------------------------------------------------------------- |
| **Tamaño (width)**                         | Ocupa todo el ancho del contenedor padre                               | Depende del contenido, pero se puede ajustar         | Depende del contenido, no se puede ajustar con width                       |
| **Posicionamiento**                        | Empieza en nueva línea; no permite elementos al lado (salvo con float) | Fluye con otros elementos; permite elementos al lado | Fluye con otros elementos; permite elementos al lado                       |
| **Se puede especificar width y height**    | Sí                                                                     | Sí                                                   | No; ignora width/height                                                    |
| **Alineación vertical (`vertical-align`)** | No                                                                     | Sí                                                   | Sí                                                                         |
| **Márgenes y padding**                     | Todos los lados respetados                                             | Todos los lados respetados                           | Solo horizontales; verticales no afectan layout (solo visualmente)         |
| **Float**                                  | -                                                                      | -                                                    | Al hacer float se comporta como block; permite márgenes y padding vertical |
What's the difference between a relative, fixed, absolute and statically positioned element?
| Tipo         | Qué hace                     | Comportamiento principal    
| **static**   | Posición por defecto         | Fluye normalmente en el documento; `top`, `right`, `bottom`, `left` y `z-index` no aplican                                                     |
| **relative** | Posición relativa a sí mismo | Se mueve respecto a su posición original, **sin afectar otros elementos**; deja espacio donde estaba                                           |
| **absolute** | Posición absoluta            | Se **remueve del flujo**; se posiciona relativo al **ancestro posicionado más cercano** o al contenedor inicial; **no afecta otros elementos** |
| **fixed**    | Posición fija                | Se **remueve del flujo**; se posiciona relativo al **viewport**; permanece en su lugar al hacer scroll                                         |
| **sticky**   | Posición “pegajosa”          | Se comporta como **relative** hasta que alcanza un umbral definido (`top`, etc.), luego se comporta como **fixed**                             |
absolute y fixed sacan el elemento del flujo, por lo que los demás elementos se “acomodan” como si no existiera.
relative mantiene el flujo original y solo mueve visualmente el elemento.
sticky combina lo mejor de relative y fixed, ideal para headers que se “pegan” al hacer scroll.
Have you played around with the new CSS Flexbox or Grid specs?
Yes. Flexbox is mainly meant for 1-dimensional layouts while Grid is meant for 2-dimensional layouts.

Flexbox solves many common problems in CSS, such as vertical centering of elements within a container, sticky footer, etc. Bootstrap and Bulma are based on Flexbox, and it is probably the recommended way to create layouts these days. Have tried Flexbox before but ran into some browser incompatibility issues (Safari) in using flex-grow, and I had to rewrite my code using inline-blocks and math to calculate the widths in percentages, it wasn't a nice experience.

Grid is by far the most intuitive approach for creating grid-based layouts (it better be!) but browser support is not wide at the moment.
Can you explain the difference between coding a website to be responsive versus using a mobile-first strategy?
Note that these two 2 approaches are not exclusive.

Making a website responsive means that some elements will respond by adapting its size or other functionality according to the device's screen size, typically the viewport width, through CSS media queries, for example, making the font size smaller on smaller devices.A mobile-first strategy is also responsive, however it agrees we should default and define all the styles for mobile devices, and only add specific responsive rules to other devices later. A mobile-first strategy has 2 main advantages:
It's more performant on mobile devices, since all the rules applied for them don't have to be validated against any media queries.
It forces to write cleaner code in respect to responsive CSS rules.
How is responsive design different from adaptive design?
| Característica          | Responsive Design                                                                  | Adaptive Design                        
| **Principio**           | Flexibilidad: un solo diseño fluido que se adapta a cualquier dispositivo          | Detección: varios diseños predefinidos según el dispositivo y características             |
| **Implementación**      | Media queries, grids flexibles, imágenes responsivas                               | Detecta dispositivo, resolución, DPI, etc., y carga el layout correspondiente             |
| **Ejemplo visual**      | Una bola que se encoge o agranda para pasar por varios aros                        | Varias bolas de tamaños diferentes, cada una para su aro específico                       |
| **Ventajas**            | Menos mantenimiento; un solo layout; se adapta automáticamente                     | Layouts optimizados para cada dispositivo; control total sobre apariencia por dispositivo |
| **Desventajas / retos** | Elegir breakpoints correctos; diseño único debe funcionar en todas las situaciones | Detección de dispositivo puede ser poco fiable; requiere mantener múltiples layouts    
Have you ever worked with retina graphics? If so, when and what techniques did you use?
Para logos e iconos, siempre que sea posible usa SVG.
Para imágenes de contenido, combina srcset con tamaños optimizados para que no afecte la carga.
No siempre usar la imagen de más alta resolución: equilibrio entre nitidez y rendimiento.
Is there any reason you'd want to use translate() instead of absolute positioning, or vice-versa? And why?
translate() is a value of CSS transform. Changing transform or opacity does not trigger browser reflow or repaint but does trigger compositions; whereas changing the absolute positioning triggers reflow. transform causes the browser to create a GPU layer for the element but changing absolute positioning properties uses the CPU. Hence translate() is more efficient and will result in shorter paint times for smoother animations.

When using translate(), the element still occupies its original space (sort of like position: relative), unlike in changing the absolute positioning.
HTML
| Concepto                 | Descripción                                    
| **Significado**          | DOCTYPE = **DOCument TYPE**. Indica el **tipo de documento** y a qué estándar sigue.                                      
| **Relación con DTD**     | DTD = **Document Type Definition**. Define cómo se deben estructurar los elementos en un tipo de documento (por ejemplo, qué etiquetas pueden ir dentro de otras). El DOCTYPE le dice al navegador **qué DTD debe usar para interpretar el HTML**.               |
| **Función principal**    | Informar al navegador qué versión de HTML se está usando para que renderice correctamente la página.                     
| **Modos de renderizado** | - **Modo estándar:** activado si el DOCTYPE es reconocido → el navegador sigue los estándares modernos. <br> - **Modo quirks (peculiaridades):** activado si no se reconoce el DOCTYPE → el navegador intenta emular viejos comportamientos para compatibilidad. |
| **Ejemplo en HTML5**     | `<!DOCTYPE html>`                                 ¿Cómo desplegar una página con contenido en varios idiomas?
| Aspecto         | Backend HTML           | API dinámico                   
| Contenido       | Llega completo en HTML | Se carga después desde la API                   |
| Flexibilidad    | Baja                   | Alta, se puede cambiar sin recargar             |
| Integración     | Cualquier página web   | Frameworks modernos (React, Vue, etc.)          |
| Tiempo de carga | Depende del servidor   | Depende del servidor + API y render en frontend |
¿Qué debes tener en cuenta al diseñar o desarrollar sitios en múltiples lenguajes?
Usar el atributo lang en tu HTML.
Dirigir a los usuarios a su idioma nativo: permitir que un usuario cambie su país/idioma fácilmente sin problemas.
El texto en imágenes basadas en ráster (por ejemplo, png, gif, jpg, etc.) no es escalable: colocar texto en una imagen sigue siendo una forma popular de obtener fuentes atractivas que no sean del sistema para mostrarlas en cualquier computadora. Sin embargo, para traducir el texto de la imagen, cada cadena de texto deberá tener una imagen separada creada para cada idioma. Cualquier cosa más que un puñado de reemplazos como este puede salirse rápidamente de control.
Palabras restrictivas/longitud de la oración: algunos contenidos pueden ser más largos cuando se escriben en otro idioma. Se debe tener cuidado con los problemas de diseño o desbordamiento en el diseño. Es mejor evitar diseñar donde la cantidad de texto crearía o rompería el diseño. El conteo de caracteres entra en juego con cosas como titulares, etiquetas y botones. Son un problema menor con el texto de flujo libre, como el texto del cuerpo o los comentarios.
Tener en cuenta cómo se perciben los colores: los colores se perciben de manera diferente en todos los idiomas y culturas. El diseño debe usar color adecuadamente.
Formato de fechas y monedas: las fechas del calendario a veces se presentan de diferentes maneras. Por ejemplo. "Mayo 31, 2012" en los Estados Unidos versus "31 de mayo de 2012" en partes de Europa.
No concatenar cadenas traducidas. No se deben hacer cosas como "La fecha de hoy es " + fecha. Se dividirá en idiomas con un orden de palabras diferente. Utilizar una cadena de plantilla con sustitución de parámetros para cada idioma en su lugar. Por ejemplo, mira las siguientes dos oraciones en español y chino respectivamente: Viajaré el {%date%} y {%date%} 我会出发. Tener en cuenta que la posición de la variable es diferente debido a las reglas gramaticales del lenguaje.
Dirección de lectura del idioma: en español, leemos de izquierda a derecha, de arriba a abajo, en japonés tradicional, el texto se lee de arriba a abajo, de derecha a izquierda.
¿Para qué sirve el atributo data-?
| Concepto               | Descripción                                      
| **Qué es**             | Son **atributos personalizados** que se agregan a cualquier elemento HTML, con el formato `data-nombre="valor"`.            
| **Propósito original** | Guardar **datos privados o adicionales** en el DOM sin usar hacks o atributos no estándar.                                
| **Uso moderno**        | Hoy en día, se prefiere **guardar los datos en JavaScript** y sincronizarlos con el DOM si es necesario, porque los usuarios pueden modificar fácilmente los `data-` desde la consola o inspección de elementos.                                                   |
| **Uso válido actual**  | - **Hooks para testing**: frameworks como Selenium o Capybara pueden usar `data-` para identificar elementos sin afectar el marcado semántico. <br> - Ejemplo: `data-test="boton-enviar"` permite encontrar el botón en tests automatizados sin necesidad de añadir clases o IDs adicionales. |
¿Consideras HTML5 como una plataforma web abierta. Cuáles son los componentes básicos de HTML5?
HTML5 se considera una plataforma abierta porque permite que cualquier desarrollador cree aplicaciones web ricas y accesibles sin depender de plugins propietarios. Está diseñado para ser un estándar universal, funcionando en distintos navegadores y dispositivos.HTML5 no solo define etiquetas nuevas, sino que ofrece APIs y capacidades que antes requerían plugins. Esto hace que la web sea más abierta, accesible y potente.
| Componente                    | Descripción                               
| **Semántica**                 | Etiquetas que describen mejor el contenido, como `<header>`, `<article>`, `<footer>`.      |
| **Conectividad**              | Nuevas formas de comunicarse con el servidor (ej. `WebSocket`, `Server-Sent Events`).      |
| **Offline y almacenamiento**  | Capacidad de almacenar datos localmente (`localStorage`, `IndexedDB`) y funcionar offline. |
| **Multimedia**                | Soporte nativo para **audio y video** (`<audio>`, `<video>`), sin plugins externos.        |
| **Gráficos y efectos 2D/3D**  | `<canvas>` y WebGL para dibujar gráficos y animaciones directamente en la web.             |
| **Rendimiento e integración** | Mejor uso del hardware, optimización de velocidad, APIs de alto rendimiento.               |
| **Acceso a dispositivos**     | Uso de cámaras, micrófonos, sensores, geolocalización y otros dispositivos.                |
| **Estilo**                    | Mejor integración con CSS3 para crear temas y estilos más sofisticados.                    |
Describe las diferenias entre cookie, sessionStorage y localStorage.
| Característica                                  | cookie                   | localStorage      | sessionStorage       | Casos de uso recomendados     
| **Iniciador**                                   | Cliente o servidor       | Cliente           | Cliente              | Cookies: almacenar información que el servidor necesita en cada solicitud, como tokens de sesión o preferencias del usuario que afectan al backend.                     |
| **Expiración**                                  | Se establece manualmente | Para siempre      | Al cerrar la ventana | localStorage: guardar preferencias de usuario, temas, configuraciones o datos que deben persistir aunque se cierre el navegador.                                        |
| **Persistente en sesiones del navegador**       | Depende de la caducidad  | Sí                | No                   | sessionStorage: mantener datos temporales de la sesión de una pestaña, como información de un formulario no enviado o estado de la interfaz mientras el usuario navega. |
| **Enviado al servidor con cada solicitud HTTP** | Sí                       | No                | No                   | Cookies: autenticación (JWT o sesión) que el servidor necesita leer en cada request.                                                                                    |
| **Capacidad (por dominio)**                     | \~4KB                    | \~5MB             | \~5MB                | localStorage/sessionStorage: almacenar listas de items, configuraciones de apps SPA, datos temporales de usuario sin sobrecargar las cookies.                           |
| **Accesibilidad**                               | Cualquier ventana        | Cualquier ventana | Misma ventana        | Cookies/localStorage: compartir datos entre pestañas; sessionStorage: datos aislados a una pestaña para seguridad o evitar conflictos.                                  |Las tecnologías mencionadas anteriormente son mecanismos de almacenamiento de clave-valor en el lado del cliente. Solo pueden almacenar valores como cadenas.
Describe las diferencias entre <script>, <script async> y <script defer>.
document.write() = peligroso con defer o async, puede borrar o romper la página.
Para scripts diferidos, mejor usar manipulación del DOM (appendChild, innerHTML, etc.) en lugar de document.write().
async y defer solo funcionan con scripts externos (src).
defer asegura ejecución en orden; async no.
<script> bloquea el renderizado hasta que se ejecuta.
 | Tipo de `<script>` | Comportamiento                                                                                                                                                     | Cuándo usarlo / Ejemplo                                                                                                                     |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `<script>`         | Bloquea el análisis del HTML, el script se descarga y ejecuta **inmediatamente**. El HTML se reanuda después de ejecutarse.                                        | Scripts que deben ejecutarse antes de que continúe el parsing del HTML, como librerías críticas que modifican el DOM inmediatamente.        |
| `<script async>`   | Se descarga en **paralelo** al HTML y se ejecuta **tan pronto esté disponible**, sin esperar al parsing completo.                                                  | Scripts **independientes** que no dependen de otros scripts ni del DOM completo, por ejemplo: analíticas, publicidad, trackers.             |
| `<script defer>`   | Se descarga en **paralelo** al HTML pero se ejecuta **después de que el HTML haya sido completamente parseado**. Múltiples scripts con defer se ejecutan en orden. | Scripts que dependen del DOM completo o necesitan que otros scripts se ejecuten en orden. Similar a poner `<script>` al final del `<body>`. |
¿Por qué generalmente es buena idea colocar los <link> de CSS entre <head></head> y <script> de JS justo antes del </body>? ¿Conoces alguna excepción?
¿Por qué generalmente es buena idea colocar los <link> de CSS entre <head></head> y <script> de JS justo antes del </body>? ¿Conoces alguna excepción?
Colocar los <link> en el <head>
 <link> dentro de <head></head> es parte de la especificación adecuada en la construcción de un sitio web optimizado. Cuando una página se carga por primera vez, el HTML y el CSS se analizan simultáneamente; el HTML crea el DOM (Modelo de objetos de documento) y el CSS crea el CSSOM (Modelo de objetos de CSS). Ambos son necesarios para crear los elementos visuales en un sitio web, lo que permite una sincronización rápida de la "primera pintura significativa". Esta representación progresiva es una categoría de optimización de sitios que se miden en puntajes de rendimiento. Poner hojas de estilo cerca de la parte inferior del documento prohíbe la representación progresiva en muchos navegadores. Algunos navegadores bloquean la representación para evitar tener que volver a pintar elementos de la página si cambian sus estilos. El usuario queda atrapado viendo una página en blanco. Otras veces puede haber flashes de contenido sin estilo (FOUC), que puede mostrar una página web sin aplicar estilo.
Colocar los <script> justo antes del </body>
Los <script> bloquean el análisis del HTML mientras son descargados y ejecutados. Colocar los scripts en la parte inferior permitirá que el HTML se analice y se muestre primero al usuario.
Una excepción para el posicionamiento de los <script> en la parte inferior es cuando el script contiene document.write(), pero hoy en día no es una buena práctica usar document.write(). Además, colocar <script> en la parte inferior significa que el navegador no puede comenzar a descargar los scripts hasta que se analice todo el documento. Esto garantiza que el código que necesita manipular elementos del DOM no arrojará errores y detendrá todo el script. Si necesitas poner algún <script> dentro del <head> por algún motivo, se debe utilizar el atributo defer, que logrará el mismo efecto de descarga diferido y ejecutará el script solo después de analizado el HTML.
¿Qué es el renderizado progresivo?
 | Técnica                                          | Qué hace                                                                                                                      | Ejemplo práctico                              
| **Carga perezosa (Lazy Loading)**                | Las imágenes o recursos solo se cargan cuando el usuario los necesita, normalmente al hacer scroll.                           | Una galería de fotos que carga cada imagen a medida que se desplaza la página.                                            |
| **Priorizar contenido visible (Above the fold)** | Se carga primero el CSS, scripts y contenido necesario para mostrar la parte visible de la página; el resto se carga después. | Mostrar un encabezado, menú y primer bloque de contenido mientras el resto del sitio se carga en segundo plano.           |
| **Fragmentos HTML asíncronos**                   | El servidor envía partes del HTML al navegador conforme se generan, en lugar de enviar todo de golpe.                         | Una página que muestra la cabecera y menú inmediatamente y va rellenando artículos mientras el back-end sigue procesando. |
Renderizado progresivo es un conjunto de técnicas para mostrar contenido de la página lo más rápido posible, incluso antes de que todos los recursos estén completamente cargados. Su objetivo principal es mejorar la percepción de velocidad para el usuario.
¿Por qué usaría el atributo srcset en una etiqueta de imagen? Explica el proceso que usa el navegador al evaluar el contenido de este atributo.
 El atributo srcset se utiliza en <img> para que el navegador elija automáticamente la imagen más adecuada según el tamaño de pantalla del dispositivo y su resolución. Esto mejora la experiencia del usuario y optimiza el rendimiento
 <img srcset="pequeño.jpg 500w, mediano.jpg 1000w, grande.jpg 2000w" src="default.jpg" alt="">
Proceso del navegador:
Calcula la relación entre el ancho del dispositivo y el ancho de cada imagen.
Selecciona la imagen cuya resolución sea la más cercana o superior a la densidad de pantalla del dispositivo.
Ejemplo:
Dispositivo de 320px ancho y resolución 1x → se elige pequeño.jpg 500w.
Dispositivo retina (2x) → se elige mediano.jpg 1000w, porque ofrece mejor calidad visual.
¿Has utilizado otros lenguajes de plantillas HTML anteriormente?
Sí, Pug (anteriormente Jade), ERB, Slim, Handlebars, Jinja, Liquid, por nombrar algunos. En mi opinión, son más o menos lo mismo y proporcionan una funcionalidad similar de escape de contenido y filtros útiles para manipular los datos que se mostrarán. La mayoría de los motores de plantillas también permiten inyectar tus propios filtros en caso de que se necesite un procesamiento personalizado antes de mostrarlos.
