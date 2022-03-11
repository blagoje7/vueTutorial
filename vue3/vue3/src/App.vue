<!-- prva upotreba funkcije za uvecanje counta pritiskom na dugme
<script setup>
import { ref } from 'vue'

const count = ref(0)

function increment() {
  count.value+=10
}
</script>

<template>
  <button @click="increment()">count is {{ count }} </button>
</template>
-->

<!-- FORM BINDINS -->
<!-- kombinovanje two way bindinga umesto :value="text" @input="onInput" stavili smo v-model="text" sto automatski
vezuje {{ text }} i input polje
<script setup>
import { ref } from 'vue'

const text = ref('')

/*function onInput(e) {
  text.value = e.target.value
}*/
</script>

<template>
  <input /*:value="text" @input="onInput"*/ v-model="text" placeholder="Type here">
  <p>{{ text }}</p>
</template>
-->


<!-- IF IFELSE truthy fasy -->
<!--
<script setup>
import { ref } from 'vue'

const awesome = ref(true)

function toggle() {
  /*
  awesome.value = !awesome.value za ne retardirane
  */
  if(awesome.value==true){
    awesome.value=false;
  }
  else{
    awesome.value=true;
  }
}
</script>

<template>
  <button @click="toggle">Toggle</button>
  <h1 v-if="awesome">Vue is awesome!</h1>
  <h1 v-else>Oh no 😢</h1>
</template>
-->

<!-- FOR / (t)=> t !== todo -->
<!--
<script setup>
import { ref } from 'vue'

// give each todo a unique id
let id = 0

const newTodo = ref('')
const todos = ref([
  { id: id++, text: 'Learn HTML' },
  { id: id++, text: 'Learn JavaScript' },
  { id: id++, text: 'Learn Vue' }
])

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value })
  newTodo.value = ''
  
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t)=> t !== todo)
}
</script>

<template>
  <input v-model="newTodo" @keyup.enter="addTodo">
  <button @click="addTodo">Add Todo</button>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
</template>
-->

<!-- Computed Property -->
<!-- ODAVDE KRENUTI SUTRA -->
<script setup>
import { ref, computed } from 'vue'

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: 'Learn HTML', done: true },
  { id: id++, text: 'Learn JavaScript', done: true },
  { id: id++, text: 'Learn Vue', done: false }
])

const filteredTodos = computed(()=> {
  return hideCompleted.value
    ? todos.value.filter((t)=> !t.done)
    : todos.value

  }
)

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <input v-model="newTodo" @keyup.enter="addTodo" />
  <button @click="addTodo">Add Todo</button>
  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>