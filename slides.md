---
theme: default
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
css: unocss
title: Welcome to Slidev
---

<div class="w-full flex justify-center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/95/Vue.js_Logo_2.svg/1200px-Vue.js_Logo_2.svg.png" width="200"/>
</div>

# Vue.js

Introducción a Vue.js

<div class="abs-br m-6 flex gap-2">
  <img src="/assets/logo.png" width="100" />
</div>

<!--
-->

---

# ¿Qué es Vue.js?

<br>

- Progressive FrontEnd framework
- SPA (Single Page Application)
- Founder - [Evan You](https://evanyou.me/) 
- Releases
  - v2 - 2.7.8
  - v3 - 3.2.37

---

# ¿Por qué Vue.js?

<br>

- Fácil de aprender 
- Liviano - 95.3Kb
- Declarative rendering
- Reactivity 
- Reusable Components
- Virtual DOM

---
layout: iframe-right
url: https://568hsd.sse.codesandbox.io/#/s1
---

# Declarative Rendering

**SFC (Single File Component)**

<br>
<div class="filename">S1.vue</div>
```vue {all|4|4,10|5|5,9|all}
<script setup>
import { reactive, ref } from 'vue'

const counter = reactive({ count: 0 })
const message = ref('Hello World')
</script>

<template>
  <h1>{{ message }}</h1>
  <p>count is: {{ counter.count }}</p>
</template>
```

---
layout: iframe-right
url: https://568hsd.sse.codesandbox.io/#/s2
clicks: 2
---

# Attribute Bindings

**v-bind directive**

<div class="filename">S2.vue</div>
```vue {all|8}
<script setup>
import { ref } from "vue";

const className = ref("title");
</script>

<template>
  <h1 v-bind:class="className">Red title</h1>
</template>

<style scoped>
.title {
  color: red;
}
</style>
```
<br>

<div v-click="2">
```html
<h1 :class="className">Red title</h1>
```
</div>

<arrow v-click="2" x2="120" y2="485" x1="150" y1="310" color="#564" width="2" arrowSize="1" />

---
layout: iframe-right
url: https://568hsd.sse.codesandbox.io/#/s3
clicks: 2
---

# Event Listeners

**v-on directive**

<div class="filename">S3.vue</div>
```vue {all|6-8,13}
<script setup>
import { ref } from 'vue'

const count = ref(0)

function increment() {
  count.value++
}
</script>

<template>
  <p>count is: {{ count }}</p>
  <button v-on:click="increment">+1</button>
</template>

```
<br>

<div v-click="2">
```html
<button @click="increment">+1</button>
```
</div>

<arrow v-click="2" x2="150" y2="465" x1="165" y1="400" color="#564" width="2" arrowSize="1" />

---
layout: iframe-right
url: https://568hsd.sse.codesandbox.io/#/s4
---

# Form Bindings

**v-model directive**

<div class="filename">S4.vue</div>
```vue {all|8}
<script setup>
import { ref } from "vue";

const text = ref("");
</script>

<template>
  <input v-model="text" placeholder="Type here" />
  <p>{{ text }}</p>
</template>
```

---
layout: iframe-right
url: https://568hsd.sse.codesandbox.io/#/s5
---

# Conditional Rendering

**v-if directive**

<div class="filename">S5.vue</div>
```vue {all|15,16}
<script setup>
import { ref } from "vue";

const hiddenMessage = ref(true);

function toggleMessage() {
  hiddenMessage.value = !hiddenMessage.value;
}
</script>

<template>
  <button @click="toggleMessage">
    {{ hiddenMessage ? "mostrar mensaje oculto" : "ocultar mensaje" }}
  </button>
  <h1 v-if="hiddenMessage">para ver el mensaje oculto presiona el botón</h1>
  <h1 v-else>Vue es increible! 👽</h1>
</template>
```

---
layout: iframe-right
url: https://568hsd.sse.codesandbox.io/#/s6
---

# List Rendering

**v-for directive**

<div class="filename">S6.vue</div>
```vue {all|13-15}
<script setup>
import { ref } from "vue";

const clientes = ref([
  { id: 1, nombre: "Juan" },
  { id: 2, nombre: "Carlos" },
  { id: 3, nombre: "Luis" },
]);
</script>

<template>
  <ul>
    <li v-for="cliente in clientes" :key="cliente.id">
      {{ cliente.nombre }}
    </li>
  </ul>
</template>
```

---
layout: iframe
url: https://plz0k4.sse.codesandbox.io/
---

# ToDo App

---
layout: iframe-right
url: https://lt15xx.sse.codesandbox.io/
---

# Computed Property

una computed property reacciona a los cambios de los estados de sus dependencias internas, cachea el resultado y las actualiza automaticamente

<br>
```js
const filteredTodos = computed(() => {
  return hideCompleted.value
    ? todos.value.filter((t) => !t.done)
    : todos.value
})
```

---
layout: iframe-right
url: https://568hsd.sse.codesandbox.io/#/s7
---

# Template Refs

**ref attribute**

<div class="filename">S7.vue</div>
```vue
<script setup>
import { ref, onMounted } from "vue";

const p = ref(null);

onMounted(() => {
  p.value.textContent = "mounted!";
});
</script>

<template>
  <p ref="p">hello</p>
</template>
```

--- 

# Lifecycle

<img src="https://vuejs.org/assets/lifecycle.16e4c08e.png" width="250" style="margin: auto" />

[Learn More](https://vuejs.org/guide/essentials/lifecycle.html)

---
layout: iframe
url: https://z1n19v.sse.codesandbox.io/
---

# ToDo App con fetching

---
layout: iframe-right
url: https://s5gg3d.sse.codesandbox.io/
---

# Watchers

Los watchers nos ayudan a crear "side effects" que se ejecutan reactivamente.

<br>
```js
import { watch } from "vue";

const selectedTodoId = ref(0);
const selectedTodoData = ref(null);

async function fetchTodoData() {
  selectedTodoData.value = null;
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/todos/${selectedTodoId.value}`
  );
  selectedTodoData.value = await res.json();
}

watch(selectedTodoId, fetchTodoData);
```

---
layout: iframe-right
url: https://568hsd.sse.codesandbox.io/#/s8
---

# Components

Un componente padre puede contener a un componente hijo. El componente hijo debe ser importado en el componente padre para poder ser usado en el template.

<br>
<div class="filename">S8.vue</div>
```vue
<script setup>
import ChildComp from "./ChildComp.vue";
</script>

<template>
  <ChildComp />
</template>
```
<br>
<div class="filename">ChildComp.vue</div>
```vue
<template>
  <h2>A Child Component!</h2>
</template>
```

---
layout: iframe-right
url: https://568hsd.sse.codesandbox.io/#/s9
---

# Component Props

Un componente hijo puede recibir parametros de entrada desde el padre

<div class="filename">S9.vue</div>
```vue
<script setup>
import { ref } from "vue";
import ChildComp from "./ChildComp2.vue";

const greeting = ref("Hello from parent");
</script>

<template>
  <ChildComp :msg="greeting" />
</template>
```
<br>
<div class="filename">ChildComp2.vue</div>
```vue
<script setup>
const props = defineProps({
  msg: String,
});
</script>

<template>
  <h2>{{ msg || "No props passed yet" }}</h2>
</template>
```

---
layout: iframe-right
url: https://568hsd.sse.codesandbox.io/#/s10
---

# Component Emits

Un componente hijo puede emitir eventos hacia compnente padre.

<div class="filename">S10.vue</div>
```vue
<script setup>
import { ref } from "vue";
import ChildComp from "./ChildComp3.vue";

const childMsg = ref("No child msg yet");
</script>

<template>
  <ChildComp @response="(msg) => (childMsg = msg)" />
  <p>{{ childMsg }}</p>
</template>
```
<br>
<div class="filename">ChildComp3.vue</div>
```vue
<script setup>
const emit = defineEmits(["response"]);

emit("response", "hello from child");
</script>

<template>
  <h2>Child component</h2>
</template>
```

---
layout: iframe-right
url: https://568hsd.sse.codesandbox.io/#/s11
---

# Slots

Otra forma en que un componente padre puede pasar data al hijo es a través de slots

<div class="filename">S11.vue</div>
```vue
<script setup>
import { ref } from 'vue'
import ChildComp from './ChildComp.vue'

const msg = ref('from parent')
</script>

<template>
  <ChildComp>Message: {{ msg }}</ChildComp>
</template>
```
<br>
<div class="filename">ChildComp4.vue</div>
```vue
<template>
  <slot>Fallback content</slot>
</template>
```

---
layout: iframe
url: https://xsdk0l.sse.codesandbox.io/
---

# ToDo App completed

---
layout: center
class: text-center
---

# Referencias

[Demos](https://codesandbox.io/s/vue-workshop-demos-j6mclp) · [ToDo App](https://codesandbox.io/s/vue-todo-app-components-xsdk0l) · [Vue.js Docs](https://vuejs.org/guide) · [Presentación](https://github.com/acastillo9/vue-workshop-slides)

---

# Challenge - The pollution App

Debido al problema de contaminación por el que atraviesa el planeta debemos estar al tanto del estado de la calidad del aire en las ciudades. Para ello se requiere crear una app que pueda obtener y mostrar información de los sensores de calidad del aire en todo el mundo.

**Criterios de Aceptación del reto:**

- Se debe poder seleccionar el pais, el estado y la ciudad sobre la cual queremos obtener información
- Para obtener los datos de los sensores debemos conectarnos a la API de [IQAir](https://www.iqair.com/us/commercial/air-quality-monitors/airvisual-platform/api)
- Se debe mostrar los datos obtenidos basados en el indice de calidad del aire para USA (aqius)
<img src="https://live.staticflickr.com/65535/48376157142_3611e41757_b.jpg">

**Nice to Have:**

- Mostrar en un mapa la localización del sensor basado en las coordenadas que la API de IQAir retorna. Para usar mapas facilmente en vue pueden usar esta librería [Vue Leaflet](https://vue2-leaflet.netlify.app/)
- Mostrar el clima de la zona donde se encuentra el sensor, esta es información que también podemos obtener de la API de IQAir
- Un buen Look and Feel
