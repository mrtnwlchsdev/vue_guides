# Vue

Framework de JavaScript utilizado para la construccion de interfaces de usuario.

- Vue es usado generalmente para la creacion de aplicaciones de una sola pagina.
- Vue puede ser utilizado para la creacion de aplicaciones full-stack que realizan peticiones HTTP a un servidor.
- Vue es popular con Node.js y Express (MEVN stack).
- Vue puede ejecutarse en el lado del servidor a traves de un framework llamado Nuxt.

## CDN

Una forma de iniciar una aplicacion de Vue es a traves de su CDN, la cual puede ser incrustada dentro de la cabecera del documento HTML.

La CDN de Vue ofrece todas las herramientas necesarias para iniciar un nuevo proyecto con Vue.

    <head>
        <script src="https://unpkg.com/vue@3">
        </script>
    </head>

## Vue CLI

Aplicacion de la terminal que permite la creacion de nuevos proyectos de Vue desde la linea de comandos.

### Instalacion Vue CLI

    $ npm install -g @vue/cli

## Crear un nuevo proyecto Vue

    $ vue create <project_name>

## Estructura de una aplicacion Vue

public\
    - index.html
    - favicon.ico

src\
    - main.js
    - Vue components

## Estructura de un componente Vue

Estructura de codigo similar al lenguaje de marcado HTML

    <template>
        <img alt="Vue Logo" src="/assets/logo.png">
        <HelloWorld />
    </template>

Codigo de JavaScript

    <script>
        import HelloWorld from './components/HelloWorld.vue';

        export default {
            name: 'App',
            components: {
                HelloWorld
            }
        }
    </script>

Estilos CSS

    <style scoped>
        /* CSS styles */
    </style>

### Componentes

Los componentes de Vue permiten organizar el codigo de una aplicacion en estructuras independientes y reutilizables.

Una aplicacion puede estar conformada de distintos componentes independientes, por ejemplo

    - Header
    - Content
    - Footer

Los componentes de Vue se localizan en la siguiente ruta y se identifican mediante la extension .vue

    /src
        /components
            Component.vue
            /...

## Props

Las props permiten que un componente recibe datos a traves de atributos.

    App.vue\
        <template>
            <Header title="App Title"/>
        </template>

    Header.vue\
        <template>
            <h1>{{title}}</h1>
        </template>

        <script>
        export default {
            props: {
                title: {
                    type: String,
                    default: ''
                }
            }
        }
        </script>

Las propiedades deben incrustarse dentro de codigo HTML usando llaves dobles {{prop_name}}.

Dentro del codigo JavaScript del componente que recibe la propiedad, debe definirse un objeto llamado props, el cual contendra otros objetos que especifican el nombre de la propiedad y a su vez su tipo y valor por defecto.

## Eventos

Los eventos son añadidos a un componente de Vue mediante la directiva @click.

El evento a ejecutar se incluye dentro del script del componente a traves de una propieadad llamada methods.

    <template>
        <button 
            @click="onClick">
            Click Me
        </button>
    </template>

    <script>
        export default {
            ...,
            methods: {
                onClick() {
                    console.log('Hello World');
                }
            }
        }
    </script>

## Datos

Una aplicacion de Vue puede contener datos a traves de una funcion llamada data.

    <script>
        export default {
            ...,
            data() {
                return {
                    tasks: []
                }
            }
        }
    </script>

La funcion data() retornara un objeto con los datos que podran ser utilizados en la aplicacion descritos como propiedades, y como valores de los mismos se asignara un valor por defecto.

La informacion contenida en la funcion data() podra ser pasada a otros componentes a traves de props.

    <template>
        <Tasks :tasks="tasks" />
    </template>

    <script>
        export default {
            ...,
            data() {
                tasks: []
            }
        }
    </script>

## Ciclos de vida

- created() :: Funcionalidad a ejecutar una vez un componente es creado. En este punto ya se tiene acceso a los datos y a los metodos de la aplicacion.

## Directiva v-for

Esta directiva permite iterar un bloque de codigo, comunmente una estructura de datos de tipo Array, para asi posteriormente insertar los datos obtenidos de la iteracion dentro de codigo HTML.

    <template>
        <ul v-for="(task,index) in tasks">
            <li>{{task.text}}</li>
        </ul>
    </template>

## Clases dinamicas

Los estilos de un componente se pueden definir de forma dinamica mediante la directiva :class

    <template>
        <section :class="{active:isActive}">Hello World</section>
    </template>

    <script>
        export default {
            data() {
                return {
                    isActive: true
                }
            }
        }
    </script>

    <style scoped>
        .active {
            color: green;
        }
    </style>

Un componente puede tener tanto estilos estaticos como dinamicos, estando estos encerrados entre llaves y separados por coma

    <template>
        <section :class="[active: isActive, static-class]">Hello World</section>
    </template>

## Emitir eventos

Esta caracteristica de Vue permite que un componente padre reciba un evento ejecutado desde un componente hijo.

La emision de eventos se logra mediante la siguiente sintaxis

    <template>
        <button @click="onDelete"></button>
    </template>

    <script>
    export default {
        return {
            ...,
            methods: {
                onDelete(param) {
                    this.$emit('event-name', param)
                }
            }
        }
    }
    </script>

Desde el componente hijo se emite un evento llamado event-name. Durante la emision del evento es posible realizar el envio de parametros.

El siguiente componente ejemplifica la recepcion del evento emitido

    <template>
        <ComponentChild @event-name="onEvent" />
    </template>

    <script>
    export default {
        return {
            onEvent(param) {
                console.log(param)
            }
        }
    }
    </script>

## Directiva v-model

Esta directiva permite asignar la entrada de datos de un usuario a una propiedad del metodo data().

    <template>
        <input type="text" v-model="name" />
    </template>

    <script>
    export default {
        data() {
            return {
                name: ''
            }
        }
    }
    </script>

## Directiva v-if

Esta directiva usada en Vue es el equivalente al uso de una estructura condicional if en JavaScript.

    <template>
        <div v-if="value">
            <p>Hello World</p>
        </div>
    </template>

Si el valor recibido por la directiva es true, se renderizara el codigo HTML del componente en el navegador.

Como complemento es posible añadir a un nuevo elemento HTML la directiva v-else, la cual renderizara dicho elemento en caso que la condicion de la directiva v-if no se cumpla.

    <div v-if="false">
        Nothing to print
    </div>
    <div v-else>
        Hello World
    </div>

## Propiedades computadas

En Vue los datos se suelen validar mediante propiedades computadas, las cuales son funciones que se ejecutan automaticamente cuando se modifica el estado de alguna propiedad.

Las propiedades computadas se agregan dentro de la propiedad computed.

    computed: {
        invalidName() {
            return this.name.length < 1
        }

        invalidLastName() {
            return this.lastName.length < 1
        }
    }

## Referencias con Vue

Para agregar una referencia a un elemento HTML se usa el atributo ref.

    <input 
        type="text"
        name="name"
        ref="name"/>

Una vez referenciado el elemento, este podra ser manipulado desde el codigo JS mediante la siguiente declaracion.

    this.$refs.name.focus()

Mediante el ejemplo anterior se define que cada vez que un formulario sea enviado, el control que contenga la propiedad ref junto al valor name, sera enfocado de forma automatica.
