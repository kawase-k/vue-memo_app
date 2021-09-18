<template>
  <div>
    <h5>List</h5>
    <ul>
      <li v-for="(memo, i) in memos" :key="i">
        <a class="memo-list" @click="transitionToEdit(i, memo)">
          {{ splitOneLine(memo) }}
        </a>
      </li>
      <!-- <p v-for="(memo, i) in memos" :key="i"> -->
        <!-- <a class="memo-list" @click="showMemo(i)">{{ memo.split('\n', 1).join() }}</a> -->
      <!-- </p> -->
    </ul>
  </div>
</template>

<script>
export default {
  props: ['memos'],

  methods: {
    transitionToEdit (id, memo) {
      this.$emit('transition', id, memo)
    },

    splitOneLine (memo) {
      return memo.split('\n')[0]
    } 
  }
  
}
</script>

<style scoped>
div{
    border: 1px solid blue
}
.memo-list {
  cursor: pointer;
  text-decoration:none;
}
</style>
