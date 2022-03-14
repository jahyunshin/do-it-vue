<template>
  <div class="input-box shadow">
    <input type="text" v-model="newItem" placeholder="Type what you have to do" @keyup.enter="addInput">
    <span class="add-container" @click="addInput">
      <i class="add-btn fa fa-plus" aria-hidden="true"></i>
    </span>

    <modal v-if="showModal" @close="showModal = false">
      <template v-slot:header><h3>경고</h3></template>
      <template v-slot:footer>
        <span @click="showModal = false">
          할 일을 입력하세요.
          <i class="close-modal-btn fas fa-times" aria-hidden="true"></i>
        </span>
      </template>
    </modal>
  </div>
</template>

<script>
import commonModal from '@/components/common/CommonModal.vue'

export default {
  name: "MainInput",
  data() {
    return {
      newItem: '',
      showModal: false
    }
  },
  methods: {
    addInput() {
      let textNewItem = this.newItem && this.newItem.trim();
      if ('' === textNewItem) {
        this.showModal = !this.showModal;
        return;
      }
      this.$emit('addInput', Date.now(), textNewItem);
      this.clearInput();
    },
    clearInput() {
      this.newItem = '';
    }
  },
  components: {
    modal: commonModal
  }
}
</script>

<style scoped>
  input:focus {
    outline: none;
  }
  .input-box {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
  }
  .input-box input {
    border-style: none;
    font-size: 0.9rem;
  }
  .add-container {
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: inline-block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
  }
  .add-btn {
    color: white;
    vertical-align: middle;
  }
</style>
