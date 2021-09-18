<template>
  <div>
    <h5>Format</h5>
    <List :memos="this.todos" @activateEditMode="activateEditMode"/>
    <Add @register="addTodo"/>

    <Edit v-if="editFlg"
    :id="editingId"
    :memo="editingMemo"
    @update="update"
    @removeMemo="removeMemo"/>
  </div>  
</template>

<script>
import List from './List.vue'
import Edit from './Edit.vue'
import Add from './Add.vue'

export default {
  data() {
    return {
      memos: null,
      editFlg: false,
      editingId: null,
      editngMemo: null,
      todos: [],
      newTodo: null,
      editNumber: 'editNumber'
    }
  },
  
  components: {
    List,
    Edit,
    Add
  },

  mounted() {
    if (localStorage.getItem('todos')) {
      try {
        this.todos = JSON.parse(localStorage.getItem('todos'))
      } catch(e) {
        localStorage.removeItem('todos')
      }
    }
  },

  methods: {
    addTodo(content) {
      if (!content) {
        return
      }

      if (!isNaN(this.editNumber)) {
        this.todos[this.editNumber] = content
        this.editNumber = 'editNumber'
      }
      else {
        this.todos.push(content)
      }
      this.newTodo = ''
      this.saveTodo()
    },

    saveTodo() {
      localStorage.setItem('todos', JSON.stringify(this.todos))
    },

    undo() {
      this.editFlg = false
      this.editingId = null
      this.editingMemo = null
    },

    update(...data) {
      const [id, memo] = data
      this.todos.splice(id, 1, memo)
      this.saveTodo()
      this.undo()
    },
    
    removeMemo(id) {
      this.todos.splice(id, 1)
      this.saveTodo()
      this.undo()
    },

    activateEditMode(...args) {
      const [id, memo] = args
      this.editFlg = true
      this.editingId = id
      this.editingMemo = memo
    },
  }
}
</script>

<style scoped>
/* div{ */
    /* border: 1px solid red */
/* } */
</style>
