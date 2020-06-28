<template>
  <v-container>
      <v-row>
        <v-col class="txt_center">
          <div class="todo_list_wrap">
            <h2>ToDo Application</h2>
          </div>
          <todoList></todoList>
        </v-col>
      </v-row>
    </v-container>
</template>

<script>
import todoList from '@/components/todoList'

export default {
    components: {
        todoList
    }
}
</script>

<style lang="sass">
.txt_center
  margin-top: 65px
.todo_list_wrap
  display: flex
  justify-content: center
  h2
    display: flex
</style>