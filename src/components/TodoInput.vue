<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" />
    <span class="addContainer" v-on:click="addTodo">
      <i class="fas fa-plus addBtn"></i>
    </span>

    <!-- use the modal component, pass in the prop -->
    <CommonModal v-if="showModal" @close="showModal = false">
      <!-- <template #header>
        <h3>custom header</h3>
      </template> -->
      <h3 slot="header">
        경고
        <i class="closeModalBtn fas fa-times" @click="showModal = false"></i>
      </h3>
      <div slot="body">아무것도 입력하지 않으셨습니다</div>
    </CommonModal>
  </div>
</template>

<script>
import CommonModal from "./common/CommonModal.vue";
export default {
  components: {
    CommonModal,
  },
  data: () => {
    return {
      newTodoItem: "",
      showModal: false,
    };
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== "") {
        //this.$emit("addTodoItem", this.newTodoItem);
        this.$store.commit("addOneItem", this.newTodoItem);
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
        console.log("");
      }
    },
    clearInput() {
      this.newTodoItem = "";
    },
  },
};
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478fb, #8763fb);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
.closeModalBtn {
  color: #42b983;
}
</style>
