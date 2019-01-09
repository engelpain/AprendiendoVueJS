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
2. [Crear una lista dinámica](#creando-una-lista-dinámica)
3. [Agregar elementos a la lista](#agregar-elementos-a-la-lista)


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

[Ejemplo de Hola mundo]("./html/holamundo.html")



### Crear una lista dinámica con un array de datos
1. Se crea un nuevo componente, llamado *appListarElementos* apuntando al selector del DOM, en la *data* del componente se agregará un array con una lista de elementos, que serán enviados al DOM usando Vue.JS:
```javascript
var appListarElementos = new Vue({
  el: '#listaDinamica',
  data: {
    listaDeElementos: [ "Primero", "Segundo", "Último" ]
  }
});
```

2. Se agrega la directiva de iteración **v-for** al selector que será impreso por la iteración de los elementos la lista, donde elemento:
```html
<div id="listaDinamica">
  <ul>
    <li v-for="elemento in listaDeElementos">
      {{ elemento }} 
    </li>
  </ul>
</div>
```

### Crear una lista dinámica con un array de objetos
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
[Ejemplo de Hola mundo]("./html/listasdinamicas.html")



### Agregar elementos a la lista
1. Tomando el ejemplo anterior de [crear una lista dinámica con un array de datos](#crear-una-lista-dinámica-con-un-array-de-datos):
```javascript
var appListarElementos = new Vue({
  el: '#listaDinamica',
  data: {
    listaDeElementos: [ "Primero", "Segundo", "Último" ]
  }
});
```

2. Hay que crear una variable dentro del componente, en este caso será denominada **nombre**, e irá vacía para poder guardar los datos que se le enviarán posteriormente:
```javascript
var appListarElementos = new Vue({
  el: '#listaDinamica',
  data: {
    listaDeElementos: ['Primero', 'Segundo', 'Último']
  },
  nombre: '',
});
```

3. Hay que crear el método **agregarNombre** que incluirá el **nombre** en el array:
```javascript
var appListarElementos = new Vue({
  el: '#listaDinamica',
  data: {
    listaDeElementos: ['Primero', 'Segundo', 'Último']
  },
  nombre: '',
  methods: {
    agregarNombre: function() {
      this.listaDeElementos.push(this.nombre);
      this.nombre = '';
    }
  },
});
```

4. En el ejemplo anterior de [crear una lista dinámica con un array de datos](#crear-una-lista-dinámica-con-un-array-de-datos), se imprimían los datos usando {{ elemento }}, en este caso se usará la directiva **v-text** que realiza la misma función:
```html
<div id="listaDinamica">
  <ul>
    <li v-for="elemento in listaDeElementos" v-text="elemento"> </li>
  </ul>
</div>
```

5. Agregar un input apuntando al modelo **nombre** y que al pulsar enter llame al método **agregaNombre**, que agregará el texto al array y luego pondrá el input en blanco de nuevo:
```html
<div id="listaDinamica">

  <ul>
    <li v-for="elemento in listaDeElementos" v-text="elemento"> </li>
  </ul>

  <input type="text" id="nombreElemento" v-model="nombre" v-on:keyup.enter="agregarNombre">

</div>
```
[Ejemplo de Hola mundo]("./html/agregarelementosalalista.html")



### Enlazar datos (Data Binding)
1. Crear la instancia de Vue apuntando a un elemento, en este caso apunta al elemento con el id **main**, dentro de data crear una variable que contendrá la información que se le envíe. 
```javascript
new Vue({
  el: '#main',
  data: {
    info: ''
  }
})
```


```html 
<div id="main">
  <input type="text" v-model="info">
  <p v-bind:title="info">Lo que manda el input: {{ info }}</p>
</div>
``` 

  <script>

  </script>