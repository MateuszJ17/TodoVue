<template>
  <div>
    <b-navbar variant="dark">
      <b-navbar-brand class="todo-nav">{{brand}}</b-navbar-brand>
    </b-navbar>

    <b-container fluid class="todo-container">
      <h3>To-do items:</h3>
      <hr style="border: 1px solid black;" />
      <TodoItems
        :title="newItemTitle"
        :description="newItemDescription"
        :isCompleted="false"
        ref="child"
      />
      <hr style="border: 1px solid black;" />
      <b-button id="show-btn" @click="showModal">Add new item</b-button>
    </b-container>

    <b-modal ref="my-modal" hide-footer title="Add">
      <div class="d-block text-center">
        <h4>Title</h4>
        <b-input v-model="newItemTitle"></b-input>
        <h4>Description</h4>
        <b-textarea v-model="newItemDescription"></b-textarea>
      </div>
      <b-button class="mt-2" variant="outline-primary" block @click="addItem">Add To-do item</b-button>
    </b-modal>
  </div>
</template>

<script>
import TodoItems from "./TodoItems";

export default {
  components: {
    TodoItems
  },

  data() {
    return {
      brand: "Todo",
      newItemTitle: " ",
      newItemDescription: " "
    };
  },
  methods: {
    showModal() {
      this.newItemTitle = " ";
      this.newItemDescription = " ";
      this.$refs["my-modal"].show();
    },
    addItem() {
      this.$refs["my-modal"].toggle("#toggle-btn");
      this.$refs.child.addItem(this.newItemTitle, this.newItemDescription);
    }
  }
};
</script>

<style>
.todo-nav {
  color: azure !important;
}

.todo-container {
  text-align: center;
  padding-left: 0px !important;
  padding-right: 0px !important;
  margin-top: 15px !important;
}
</style>
