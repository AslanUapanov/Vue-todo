<template>
<v-container>
  <v-row>
    <v-col md="3"></v-col>
    <v-col class="todo_wrap" md="6">
      <div class="input_todo">
        <div class="input_todo_head">
          <v-input>
            <v-text-field @keyup.enter="addTodo" label="Add todo" v-model="value"></v-text-field>
          </v-input>
          <v-btn @click="addTodo"  class="mx-2" fab dark color="indigo">
            <v-icon dark>mdi-plus</v-icon>
          </v-btn>
        </div>
        <div class="select_todo">
          <select v-model="selected" label="Filter todo">
          <option v-for="option in filterTodo" :key="option.id" :value="option.value">
            {{ option.text }}
          </option>
          </select>
        </div>
      </div>
      <div>
        <ul >
          <draggable v-model="todo"
            class="block_todo"
            ghost-class="ghost"
            :sort="true"
            @start="dragging = true"
            @end="dragging = false"
          >
            <todo v-for="(todos, index) of filetered" @removeTodo="removeTodo" :todoItem="todos" :key="index"></todo>
          </draggable>
        </ul>
      </div>
    </v-col>
    <v-col md="3"></v-col>
  </v-row>
</v-container>

</template>
<script>
import todo from './todoItem'
import draggable from 'vuedraggable'
export default {
  data: () => ({
    value: '',
    selected: '1',
    todo: [],
    removedTodo: [],
    filterTodo: [
      {
        text: 'All',
        value: 1
      },
      {
        text: 'Completed',
        value: 2
      },
      {
        text: 'Not completed',
        value: 3
      }
      ],
    i: '1',
    checkbox: false,
    dragging: false,
    showEdit: false,
    showText: true
  }),
  methods: {
    addTodo(){
      if(this.value !== ""){
        this.todo.push({text: this.value, id: this.i, checkbox: this.checkbox, showText: this.showText, showEdit: this.showEdit})
        this.value = ""
        this.i = this.i + 1
      }
    },
    removeTodo(id){
      this.todo = this.todo.filter(t => t.id !== id)
    },
  },
  computed: {
    filetered(){
      if(this.selected == 1){
        return this.todo
      }

      if(this.selected == 2){
        return this.todo.filter(t => t.checkbox)
      }

      if(this.selected == 3){
        return this.todo.filter(t => !t.checkbox)
      }
    }
  },
  components: {
      todo,
      draggable
  }
}
</script>
<style lang="sass" scoped>
.ghost
  opacity: 0.7
  border: 1px solid #fff
  background-image: linear-gradient(120deg, #d4fc79 0%, #96e6a1 100%)
  padding-left: 20px
  transform: scale(0.9)
  transition: top 1s ease-out 0.5s
.input_todo
  display: flex
  justify-content: center
  flex-direction: column
.input_todo_head
  display: inline-flex
.select_todo
  display: flex
  justify-content: center
ul
  list-style-type: none
.block_todo
  display: flex
  flex-direction: column
  align-items: center
  justify-content: center
  
.todo_wrap
  display: flex
  flex-direction: column
  justify-content: center
</style>