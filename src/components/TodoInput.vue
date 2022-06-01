<template>
  <div class="inputBox">
    <input type="text" v-model="newTodoItem" placeholder="Type what you have to do"
    @keyup.enter="addTodo">
    <span class="addContainer" @click="addTodo">
      <i class="addBtn fas fa-plus" aria-hidden="true"></i>
    </span>
    <Modal :show="showModal" @close="showModal = false" />
  </div>
</template>

<script>
import Modal from "./common/Modal.vue"
export default {
  data() {
    return {
      newTodoItem : '',
      showModal : false
    }
  },
  methods : {
    addTodo() {
      if(this.newTodoItem !== '') {
        var value = this.newTodoItem && this.newTodoItem.trim()
        this.$emit('addTodo', value)
        this.clearInput();
      } else {
        this.showModal = !this.showModal
      }
    },
    clearInput() {
      this.newTodoItem = ''
    }
  },
  components : {
    Modal
  }
}
</script>

<style scoped>
  input:focus {  /*:focus 선택자 : 선택하는 순간 적용되는 css */
    outline: none;
  }
  .inputBox {
    background : white;
    height : 50px;
    line-height : 50px; /*line-height : 글자 위아래 여백*/ 
    border-radius: 5px;
  }
  .inputBox input {
    border-style: none;
    font-size: 0.9rem;
  }
  .addContainer {
    float : right; /* float 이미지 어디에 위치시켜서 텍스트랑 보여줄 것인지 설정 */
    background : linear-gradient(to right, #6478fb, #8763fb); /* 그라데이션 (진행방향, 색상1, 색상2 ..) */
    display : block;
    width : 3rem; /* 상대적인 크기를 정하는 단위 */
    border-radius: 0 5px 5px 0;
  }
  .addBtn {
    color : white;
    vertical-align: middle;
  }
</style>