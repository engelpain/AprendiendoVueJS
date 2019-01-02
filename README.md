## Aprendiendo a usar VueJS
Centro Nacional de Desarrollo e Investigación de Tecnologías Libres (CENDITEL) <br>
[CENDITEL](https://www.cenditel.gob.ve/), Mérida - Venezuela<br>
Dirección de Desarrollo<br>
Autor: [Ing. Angelo Osorio](https://twitter.com/Engel_PAIN)<br>
Fecha de Elaboración: 29-12-2018 (dd,mm,aaaa)

### [VueJS](https://vuejs.org/)
Vue es un framework progresivo para la creación de interfaces de usuario. A diferencia de otros frameworks monolíticos, Vue está diseñado desde cero para que pueda ser adoptado gradualmente. La librería central se enfoca solo en la capa de vista y es fácil de captar e integrar con otras librerías o proyectos existentes. Por otro lado, Vue también es perfectamente capaz de impulsar aplicaciones sofisticadas de una sola página cuando se usa en combinación con herramientas modernas y librerías de soporte.

Para enlazar el framework a un proyecto:

```html
<!-- Versión de desarrollo -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

<!-- Versión de producción -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

### Mi primera aplicación con Vue
1. [Escribir texto en el DOM](#escribir-texto-en-el-dom)
2. [Creando una lista dinámica](#creando-una-lista-dinamica)


### Escribir texto en el DOM
1. Se agrega un *selector* (puede ser cualquier selector, *tag*, *#id*, *.class*), donde se imprimirá la información.
El selector en este ejemplo, tiene el *id* __selectorDOM__, y será utilizado por el componente para asociarlo con la infomación que será enviada a este.
```html
<main id="selectorDOM">
</main>
```


2. Se crea la aplicación con VueJS:
```javascript
/** nuevaAplicacion
  * Para desarrollar una aplicación con VueJS, se debe crear una instancia del objeto Vue.
  *
  * @param el:     (selector del DOM donde se cargará la aplicación)
  * @param data:   (información que será enviada al DOM)
  */
  var nuevaAplicacion = new Vue({
    el: '#selectorDOM',
    data: {
      mensaje: 'Hola mundo!'
    }
  })
```


3. En el paso dos se declaró la *data* que será enviada al DOM por el componente. Ahora hay que añadirla al selector:
```html
<main id="selectorDOM">
  {{ mensaje }}
</main>
```


### Creando una lista dinámica
1. Se crea un nuevo componente, llamado *appListarElementos* apuntando al selector del DOM, en la *data* del componente se agregará un array con una lista de elementos, que serán enviados al DOM usando Vue.JS:
```javascript
var appListarElementos = new Vue({
  el: '#listaDinamica',
  data: {
    listaDeElementos: [
      { texto: 'Primer elemento de la lista'},
      { texto: 'Segundo elemento de la lista' },
      { texto: 'Último elemento de la lista' },
    ]
  }
});
```

2. Se agrega la directiva de iteración **v-for** al selector que será impreso por la iteración de los elementos la lista, donde elemento:

```html
<div id="listaDinamica">
  <ul>
    <li v-for="elemento in listaDeElementos">
      {{ elemento.texto }} 
    </li>
  </ul>
</div>
```