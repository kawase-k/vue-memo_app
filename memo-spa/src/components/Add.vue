<template>
  <div>
    <h5>Add</h5>
    <button v-if="!addFlg" @click="registerMemo">＋</button>

    <div v-if="addFlg">
      <textarea v-model="newMemo" type="text" placeholder="Add new..."></textarea>
      <button @click="addMemo">Add</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      addFlg: false,
      newMemo: null
    }
  },

  methods: {
    registerMemo() {
      this.addFlg = !this.addFlg
    },

    addMemo() {
      this.$emit('add', this.newMemo)
      this.addFlg = false
      this.newMemo = ''
    }
  }
}
</script>

<style scoped>
div{
    border: 1px solid rgb(255, 0, 212) 
}
</style>
