<template>
  <div class="clear-all-container">
    <span class="clear-all-btn" @click="clearTodo">Clear All</span>
  </div>
</template>

<script>
export default {
  methods: {
    clearTodo() {
      this.$emit('removeAll');
    }
  }
}
</script>

<style>
  .clear-all-container {
    width: 8.5rem;
    height: 50px;
    line-height: 50px;
    background-color: white;
    border-radius: 5px;
    margin: 0 auto;
  }

  .clear-all-btn {
    color: #e20303;
    display: block;
  }
</style>
