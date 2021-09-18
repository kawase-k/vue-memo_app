<template>
  <div>
    <h5>Add</h5>
    <button v-if="!registerFlg" @click="toggleRegister">Add</button>

    <div v-if="registerFlg">
      <textarea v-model="newMemo"></textarea>
      <button @click="register">Reg</button>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      registerFlg: false,
      newMemo: null
    }
  },

  methods: {
    toggleRegister () {
      this.registerFlg = !this.registerFlg
    },
    register () {
      this.$emit('register', this.newMemo)
      this.newMemo = ''
      this.registerFlg = false
    }
  }
}
</script>

<style scoped>
div{
    border: 1px solid rgb(255, 0, 212) 
}
</style>
