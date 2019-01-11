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
1. [Enlazar datos - Data Binding](#enlazar-datos-data-binding))
1. [Condicionales - 1ra Parte](#condicionales---1ra-parte)
1. [Modelo de datos](#modelo-de-datos)
1. [Crear una lista dinámica](#crear-una-lista-dinámica)
1. [Agregar elementos a la lista](#agregar-elementos-a-la-lista)
1. [Ajax en VueJS con Vue resource](#ajax-en-vuejs-con-vue-resource)
1. [Ajax en VueJS con Axios](#ajax-en-vuejs-con-axios)
1. [V-Show](#v-show)
1. [Condicionales - 2da Parte](#condicionales---2da-parte)


### Escribir texto en el DOM
1. Se agrega un *selector* (puede ser cualquier selector, *tag*, *#id*, *.class*), donde se imprimirá la información.
El selector en este ejemplo, tiene el *id* __selectorDOM__, y será utilizado por el componente para asociarlo con la infomación que será enviada a este.
```html
<main id="selectorDOM">
</main>
```

2. Se crea la aplicación con VueJS:
```javascript
/** saludar
  * Para desarrollar una aplicación con VueJS, se debe crear una instancia del objeto Vue.
  *
  * @param el:     (selector del DOM donde se cargará la aplicación)
  * @param data:   (información que será enviada al DOM)
  */
  var saludar = new Vue({
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
Demo: [Escribir texto en el DOM](./html/holamundo.html)



### Enlazar datos - Data Binding
> Directiva v-bin:propiedad - Permite agregar, modificar y eliminar propiedades a elementos en el DOM.
> Otra forma de agregar binding al DOM es usandola expresión {{ elemento }}, donde dato es el dato que se quiere imprimir.

Imprimir un dato con data binding es tan sencillo como:
```html
<div id="main">
  {{ dato }}
</div>
```

Permite usar todo el poder de JavaScript en expresiones, por ejemplo, para hacer una suma, solo se usaría la expresión del data binding, y ella se encargará de devolver el resultado:
```html
<div id="main">
  {{ 1 + 2 }}
</div>
```

Se pueden modificar valores de atributos de un elemento:
```html
<div id="main">
  <input type="text" v-bind:style="color" v-bind:value="valorDelInput" >
</div>
```

También se puede escribir la sintaxis de forma corta:
```html
<div id="main">
  <!-- full syntax -->
  <p v-bind:style="color"> Sintaxis larga </p>

  <!-- shorthand -->
  <p :style="color"> Sintaxis corta </p>
</div>
```

#### Usando lo aprendido
1. Crear el componente Vue, dentro de *data* crear las variables que contendrán las propiedades que se le asignarán al elemento:
```javascript
var binding = new Vue({
  el: '#main',
  data: {
    valorDelInput: 'Texto de ejemplo',
    color: 'color: #00f',
  }
})
```

2. Agregar el elemento destino, dentro crear dos elementos, un input apuntando al modelo y en el otro se imprimirá en tiempo real lo que trae el componente 
```html
<div id="main">
  <input type="text" v-bind:style="color" v-bind:value="valorDelInput" >
</div>
```
Demo: [Enlazar datos (Data Binding)](./html/databinding.html)



### Condicionales - 1ra Parte
> Directiva v-if - Permite manipular elementos dependiendo del valor de la variable que se está evaluando

1. Crear el componente con una variable booleana que definirá si se muestra el texto del elemento en el DOM
```javascript
var condicionalIf = new Vue({
  el: '#condicional',
  data: {
    // Si se cambia a false, desaparecerá el elementos del DOM
    verTexto: true
  }
})
```

2. Añadir la directiva **v-if** al elemento destino del DOM
```html
<div id="condicional">
  <span v-if="verTexto">Ahora me puede ver</span>
</div>
```
Demo: [Condicional](./html/condicional.html)



### Modelo de datos
> Directiva v-model - Permite agregar, modificar y eliminar el valor de un variable.

1. Crear el componente Vue, dentro de *data* crear una variable que contendrá la información que se le envíe:
```javascript
var enviarDatos = new Vue({
  el: '#elementoReceptor',
  data: {
    informacion: ''
  }
});
```

2. Agregar el elemento destino, dentro crear dos elementos, un input apuntando al modelo y en el otro se imprimirá en tiempo real lo que trae el componente 
```html 
<main id="elementoReceptor">
  <input type="text" v-model="informacion">
  <p>Lo que manda el input: {{ informacion }}</p>
</main>
```
Demo: [Modelo de datos](./html/modelodedatos.html)


### Crear una lista dinámica
> Directiva v-for - Permite hacer iteraciones de arrays guardados en el *data* del componente.

#### Con un array de datos

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

#### Con un array de objetos

1. Se crea un nuevo componente, llamado *appListarElementos* apuntando al selector del DOM, en la variable *data* del componente se agregará un array con una lista de elementos, que serán enviados al DOM usando Vue.JS:
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
Demo: [Lista dinámica](./html/condicional.html)



### Agregar elementos a la lista
1. Tomando el ejemplo anterior de [Con un array de datos con un array de objetos](#con-un-array-de-datos):
```javascript
var appListarElementos = new Vue({
  el: '#listaDinamica',
  data: {
    listaDeElementos: [ "Primero", "Segundo", "Tercer" ]
  }
});
```

2. Crear una variable dentro de _data_, donde se guardarán los datos enviados desde el input:
```javascript
var appListarElementos = new Vue({
  el: '#listaDinamica',
  data: {
    listaDeElementos: ['Primero', 'Segundo', 'Tercer'],
    nombre: '',
  },
});
```

3. Crear el método _agregarNombre_ que incluirá el _nombre_ en el array _listaDeElementos_:
```javascript
var appListarElementos = new Vue({
  el: '#listaDinamica',
  data: {
    listaDeElementos: ['Primero', 'Segundo', 'Tercer'],
    nombre: '',
  },
  methods: {
    agregarNombre: function() {
      this.listaDeElementos.push(this.nombre);
      this.nombre = '';
    }
  },
});
```

4. En el ejemplo anterior de [crear una lista dinámica con un array de datos](#con-un-array-de-objetos), se imprimían los datos usando {{ elemento }}, en este caso se usará la directiva **v-text** que realiza la misma función:
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
Demo: [Agregar elementos a la lista](./html/agregarelementosalalista.html)



### Ajax en VueJS con Vue resource
> Recomendada para usuarios de VueJS 1

Demo: [Ajax en VueJS con Vue resource](./html/ajaxconresource.html)



### Ajax en VueJS con Axios
> Recomendada por VueJS para la versión 2

Demo: [Ajax en VueJS con Axios](./html/ajaxconaxios.html)



### V-Show
> Directiva v-show - muestra u oculta elementos dependiendo de si existen o no.

Para demostrar para qué funciona v-show, se hará un ejemplo práctico que mantendrá oculto el botón de _submit_ de un formulario, hasta que se llene el campo input:

1. Se crea el componente con un modelo llamado *email*:
```javascript
var enviarDatos = new Vue({
  el: '#mostrarElemento',
  data: {
    email: ''
  }
});
```

2. Crear un formulario, al botón _submit_ se le agrega la directiva **v-show** que estará enlazada al valor del modelo _email_, y que se mostrará solo cuando se haya introducido al menos un valor en el input que apunta a ese modelo. 
```html
<main id="mostrarElemento">
  <input type="text" v-model="email"/>
  <input type="submit" v-show="email">
</main>
```
Demo: [Directiva v-show](./html/vshow.html)



### Condicionales - 2da Parte
> Directiva v-if y v-else - Se usa para manipular elementos del DOM dependiendo del valor de la variable que se condiciona.

La directiva **v-if** tiene una contraparte denominada **v-else**, que se mostrará en caso de que no se cumpla la condición de **v-if**:

```
<!-- Si no existe un mensaje, se muestra este texto -->
<p v-if="!mensaje"> No hay mensaje</p>

<!-- En caso contrario, se muestra este texto -->
<p v-else> Hay un mensaje: {{ mensaje}}</p>
```

> **v-else** está enlazado al **v-if** contiguo a este, por lo que si se quiere mostrar más de un mensaje no se deben declarar muchas veces el if sino usar la etiqueta <template> y dentro guardar 
lo que se enviará.

#### Usar las directivas:

##### JS
```javascript
var mostrarTextoCondicional = new Vue({
  el: '#app',
  data: {
    mensaje: ''
  }
})
```

##### html

```html
<main id="app">
  <!-- En lugar de abrir muchos v-if, se utiliza la etiqueta template -->
  <template v-if="!mensaje">
    <!-- Este texto se mostrará si no existe un mensaje en el modelo -->
    <h3>Escriba un mensaje</h3>
    <p>Cualquier cosa será válida</p>
  </template>

  <!-- De igual forma con el v-else -->
  <template v-else>
    <!-- Este texto se mostrará si existe un mensaje en el modelo -->
    <h3>Presione enter para enviar el mensaje</h3>
    <p>Qué interesante</p>
  </template>

  <!-- Textarea enlazado a mensaje para ver el cambio en tiempo real -->
  <textarea cols="30" rows="10" v-model="mensaje"></textarea>

  <!-- Muestra el json que devuelve data, es solo informativo -->
  <pre>
    {{ $data }}
  </pre>
</main>
```

Demo: [v-if y v-else](./html/vifyvelse.html)