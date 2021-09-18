<template>
  <div>
    <h5>Form</h5>
    <textarea v-model="editingMemo" type="text" placeholder="New change..."></textarea>
    <button @click="editMemo">Update</button>
    <button @click="removeMemo">Delete</button>
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
  
  methods: {
    editMemo() {
      this.$emit('editMemo', this.editingId, this.editingMemo)
      this.undo()
    },

    removeMemo() {
      if (confirm('このメモを削除しますか？')) {
        this.$emit('removeMemo', this.editingId)
        this.undo()
      }
    },

    undo() {
      this.editingId = null
      this.editingMemo = null
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
