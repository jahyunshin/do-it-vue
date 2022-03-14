<template>
  <section>
    <transition-group name="list" tag="ul">
      <li v-for="(item, index) in listItems" :key="item" class="shadow" :id="item.key">
        <i class="check-btn fas fa-check" aria-hidden="true"></i>
          {{ item.value }}
        <span class="remove-btn" type="button" @click="removeTodo(item.key, index)">
          <i class="far fa-trash-alt" aria-hidden="true"></i>
        </span>
      </li>
    </transition-group>
  </section>
</template>

<script>
export default {
  props: ['listItems'],
  methods: {
    removeTodo(key, index) {
      this.$emit('removeList', key, index);
    }
  }
}
</script>

<style>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.check-btn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.remove-btn {
  margin-left: auto;
  color: #de4343;
}

.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
