<template>
  <div class="testing">
    <i>Press enter</i>
    <br />
    <form v-on:submit.prevent>
      <input v-on:keypress="submit" type="text" v-model="name" />
    </form>
    <ul>
      <li
        v-for="(item, index) in data"
        v-bind:key="index"
        :class="{'red': (item === isChecked(item))}"
      >
        <input v-model="checked" :value="item" type="checkbox" />
        <span>{{item}}</span>
        <a
          href="#"
          v-on:click.prevent="(item === isChecked(item)) ? deleteItem(index):myfunciton()"
        >Delete</a>
        <a href="#" v-on:click.prevent="editItem(index)">Edit</a>
      </li>
    </ul>
  </div>
</template>

<script>
import Vue from "vue";

export default {
  name: "Test",
  data: function() {
    return {
      name: "",
      data: [],
      editIndex: false,
      isRed: false,
      checked: []
    };
  },
  methods: {
    submit: function(e) {
      if (e.keyCode === 13) {
        if (this.editIndex) {
          // this.data.splice(this.editIndex,1,this.name);
          //split also works fine, but just trying out Vue.set
          Vue.set(this.data, this.editIndex, this.name);
          this.name = "";
          this.editIndex = -1;
        } else {
          this.data.push(this.name);
          this.name = "";
        }
      }
    },

    deleteItem: function(index) {
      this.data.splice(index, 1);
    },

    editItem: function(index) {
      this.editIndex = index;
      this.name = this.data[index];
    },

    isChecked(item) {
      return this.checked.find(el => el == item);
    },

    myFunction() {
      alert("Please select to delete");
    }
  }
};
</script>

<style>
.red {
  color: red;
}

.testing li {
  border: 1px solid;
  padding: 5px;
}

.testing li a {
  font-size: 10px;
  float: right;
  padding: 5px;
}
</style>
