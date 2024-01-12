# Vue3js Crash Course

## Conditional Rendering

* can use v-if, v-else inline in the template

## Passing Props

* Make sure to update the value of the prop in the component where the data is created

* dont update the prop in the child component

* listen for the change and emit an event in the child

* listen for the emit in the parent

### first make sure that in your model you have a identifier for your piece of data. and make sure you are passing the proper identifier. ie. if it is a list pass an index.

const props = defineProps({

    todo: {

        type: Object,

        required: true,

    },

    index: {

      type: Number,

      required: true,

    }
})

<TodoItem `v-for="(todo, index) in todoList"` :todo="todo" :index="index" @toggle-complete="toggleTodoComplete" />

### pass the index as a prop to your child

<TodoItem v-for="(todo, index) in todoList" `:todo="todo" :index="index`" @toggle-complete="toggleTodoComplete" />

### in your child component define an emit on input change

<input `@input=`"$emit('toggle-complete', index)" type="checkbox" :checked="todo.isCompleted" />

### define the emit in the `script` of the child component

`defineEmits(["toggle-complete"]);`

### Listen for the emit in your parent component and call a function that you are about to create in the script

<TodoItem v-for="(todo, index) in todoList" :todo="todo" :index="index" `@toggle-complete=`"toggleTodoComplete" />

### set it to the function that you want the emit to trigger
<TodoItem v-for="(todo, index) in todoList" :todo="todo" :index="index" @toggle-complete=`"toggleTodoComplete"` />

### create the function to change the value in the script of the parent 

`const toggleTodoComplete = (todoPos) => {
  todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted
};`

### now in the child component you can add conditional styles etc

<span v-else `:class="{'completed-todo' : todo.isCompleted}"`>
