<template>
  <div>
    {{ msg }}
    <form>
      <button @click="addTodo()">Add a Task</button>
      <button @click="removeTodo()">Delete Finished Tasks</button>
      <p>input:<input type="text" v-model="newTodo"></p>
      <p>task:{{newTodo}}</p>
    </form>
    <div class="task-list">
      <label class="task-list__item" v-for="todo in todos" v-bind:class="{'task-list__item--checked':todo.done}">
        <input type="checkbox" v-model="todo.done">
        <input type="checkbox" v-model="todo.editing">
        <input v-if="todo.editing" v-model="todo.text" @keyup.enter="todo.editing = !todo.editing">
        <span v-else>{{todo.text}}</span>
      </label>
    </div>

    <h2>References</h2>
    <ul>
      <li>
        <a
          href="https://qiita.com/sin_tanaka/items/29769266b3b078ea0f7c"
          target="_blank"
        >
          vue-cliで始めるVue.jsチュートリアル (1)
        </a>
      </li>
      <li>
        <a
          href="https://qiita.com/sin_tanaka/items/6d5d9089eb76dda4ce88"
          target="_blank"
        >
          vue-cliで始めるVue.jsチュートリアル (2)
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      todos:[
        {text: 'vue-router',done:false,editing:false},
        {text: 'vuex',done:false,editing:false},
        {text: 'vue-loader',done:false,editing:false},
        {text: 'awesome-vue',done:true,editing:false},
      ],
      newTodo:""
    }
  },
  methods:{
    addTodo: function(event){
      let text = this.newTodo && this.newTodo.trim()
      if(!text){
        return
      }
      this.todos.push({text:text,done:false,editing:false})
      this.newTodo=''
    },
    removeTodo: function(event){
      for(let i = this.todos.length-1;i>=0;i--){
        if(this.todos[i].done)this.todos.splice(i,1)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@mixin flex-vender(){
  display: flex;
  display: -webkit-flex;
  display: -moz-flex;
  display: -ms-flex;
  display: -o-flex;
}

.task-list{
  @include flex-vender;
  flex-direction: column;
  align-items: center;
  &__item{
    width: 270px;
    text-align: left;
    $element: #{&};
    &--checked{
      @extend #{$element};
      color: #85a6c6;
    }
  }
}
</style>
