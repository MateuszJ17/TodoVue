<template>
  <div>
    <b-row
      class="item-row"
      v-for="item in items"
      v-bind:key="item.id"
      v-bind:class="{completed: item.isCompleted}"
    >
      <b-col cols="1">{{item.id}}</b-col>
      <b-col>{{item.title}}</b-col>
      <b-col cols="6">{{item.description}}</b-col>
      <b-col></b-col>
      <b-col>
        <b-button class="item-btn" size="sm" v-on:click="deleteItem(item.id)">Delete</b-button>
        <b-button class="item-btn" size="sm" v-on:click="changeComplete(item.id)">Completed</b-button>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import json from "../../resources/todos.json";

export default {
  props: {
    title: String,
    description: String,
    isCompleted: Boolean
  },

  data() {
    return {
      itemID: this.id,
      itemTitle: this.title,
      itemDescr: this.description,
      items: json
    };
  },

  methods: {
    deleteItem(id) {
      this.items = this.items.filter(function(itm) {
        return itm.id != id;
      });
    },
    changeComplete(id) {
      this.items.forEach(itm => {
        if (itm.id === id) {
          itm.isCompleted = !itm.isCompleted;
        }
      });
    },
    addItem(ttl, descr) {
      if (this.itemTitle != "" && this.itemDescr != "") {
        this.items.push({
          id: this.items.slice(-1)[0].id + 1,
          title: ttl,
          description: descr,
          isCompleted: false
        });
      }
    }
  }
};
</script>

<style>
.item-row {
  margin-left: 0px !important;
  margin-right: 0px !important;
  padding-left: 0px !important;
  padding-right: 0px !important;
}

.item-btn {
  margin: 2px !important;
}

.item-hr {
  border: 1px solid black;
}

.completed {
  text-decoration: line-through !important;
  background-color: rgb(199, 189, 189);
}
</style>
