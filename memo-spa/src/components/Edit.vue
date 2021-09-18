<template>
  <div>
    <h5>Edit</h5>
    <textarea v-model="editingMemo" id="target" type="text" placeholder="Add new..."></textarea>
    <button @click="update">Update</button>
    <button @click="removeMemo">Delete</button>
    <p>{{ id }}: {{ memo }}</p>
  </div>  
</template>

<script>
export default {
  data() {
    return {
      editingMemo: this.memo,
      editingId: this.id
    }
  },
  
  props: ['id', 'memo'],
  
  // mounted() {
    // if (localStorage.getItem('todos')) {
      // try {
        // this.todos = JSON.parse(localStorage.getItem('todos'))
      // } catch(e) {
        // localStorage.removeItem('todos')
      // }
    // }
  // },

  methods: {
    addTodo() {
      if (!this.newTodo) {
        return
      }

      if (!isNaN(this.editNumber)) {
        this.todos[this.editNumber] = this.newTodo
        this.editNumber = 'editNumber'
      }
      else {
        this.todos.push(this.newTodo)
      }
      this.newTodo = ''
      this.saveTodo()
    },

    saveTodo() {
      localStorage.setItem('todos', JSON.stringify(this.todos))
    },

    update() {
      this.$emit('update', this.editingId, this.editingMemo)
      this.editingId = null
      this.editingMemo = null
    },

    removeMemo() {
      if (confirm('このメモを削除しますか？')) {
        this.$emit('removeMemo', this.editingId)
        this.editingId = null
        this.editingMemo = null
      }
    }
  },
  
  watch: {
    id: function (newId) {
      this.editingId = newId
    },
    memo: function (newMemo) {
      this.editingMemo = newMemo
    }
  }
}
</script>

<style scoped>
div{
    border: 1px solid green
}
</style>
