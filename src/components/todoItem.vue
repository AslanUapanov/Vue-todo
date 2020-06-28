<template>
    <li>
      <div class="chekbox_block">
        <v-checkbox v-model="todoItem.checkbox" color="green"></v-checkbox>
      </div>
      <div :class="todoItem.checkbox == true ? 'line' : '' ">
        <div v-if="todoItem.showText">{{todoItem.text}}</div>
        <div class="todoItem_input">
          <v-input class="input" v-if="todoItem.showEdit" >
            <v-text-field @keyup.enter="editTodo" label="Edit todo" v-model="todoItem.text"></v-text-field>
          </v-input>
        </div>
      </div>
      <div class="todoBtn">
        <img @click="$emit('removeTodo', todoItem.id)" class="del_btn" src="@/assets/icon/del_icon.png" alt="" />
        <img @click="editTodo" class="edit_btn" src="@/assets/icon/edit.png" />
      </div>
    </li>
</template>
<script>
export default {
    data: () => ({
        line: 'line'
    }),
    methods: {
     editTodo(){
      this.todoItem.showEdit = !this.todoItem.showEdit
      this.todoItem.showText = !this.todoItem.showText
    }
    },
    props: ['todoItem', 'index']
}
</script>
<style lang="sass" scoped>
.line
  text-decoration: line-through
li
  display: inline-flex
  justify-content: space-between
  align-items: center
  border: 1px solid #000
  margin: 10px
  cursor: pointer
  width: 100%
.edit_btn
  cursor: pointer
  width: 25px
  height: 25px
.del_btn
  cursor: pointer
  width: 35px
  height: 35px
  margin-right: 25px
.todoBtn
  display: flex
  justify-content: center
  align-items: center
  padding-right: 20px
.chekbox_block
  display: flex
  justify-content: flex-start
  align-items: center
  padding-left: 20px
.todoItem_input
  display: flex
  justify-content: center
  align-items: center
.input
  padding-top: 5px
.v-text-field__details
  display: none!important
</style>