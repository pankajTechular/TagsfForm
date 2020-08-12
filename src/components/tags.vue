
<template>
  <div class="main-section container-fluid">
    <div class="row">
      <div class="col-md-3"></div>
      <div class="form-section col-md-6">
        <div class="heading">
          <h1>Form</h1>
        </div>
        <b-alert v-if="isSubmitted" show dismissible fade>Successfully saved you data</b-alert>

        <div class="form-group">
          <label for="message">Your Message</label>
          <textarea id="message" rows="5" class="form-control" v-model="message"></textarea>
        </div>
        <div class="form-group">
          <label for="priority">Users</label>
          <select id="priority" class="form-control" v-model="selectedUser">
            <option value>Select User</option>
            <option v-for="user in users" v-bind:key="user.id">{{ user.value }}</option>
          </select>
        </div>
        <br />

        <div class="form-group">
          <label for="tags">select tag</label>
          <vue-tags-input
            v-model="tag"
            :tags="tags"
            :autocomplete-items="filteredItems"
            @tags-changed="newTags => tags = newTags"
          />
        </div>
        <br />
        <button class="btn btn-primary" @click.prevent="submitted">Submit!</button>
      </div>
      <!-- <div class="col-md-6">
        <div class="card" v-if="isSubmitted">
          <div class="card-body">
            <h4 class="card-title">Form Data</h4>

            <p>
              Mail:
              <b>{{ userData.email }}</b>
            </p>
            <p>
              Password:
              <b>{{ userData.password }}</b>
            </p>

            <p style="white-space: pre">
              Message:
              <b>{{ message }}</b>
            </p>

            <p>
              Priority:
              <b>{{ selectedPriority }}</b>
            </p>
            <div>
              tags:
              <ul style="display:inline-block" v-bind:key="tag.id" v-for="tag in tags">
                <li>{{tag.text}}</li>
              </ul>
            </div>
          </div>
        </div>
      </div>-->
    </div>
  </div>
</template>
<script>
import Vue from "vue";
import { BootstrapVue } from "bootstrap-vue";
import VueTagsInput from "@johmun/vue-tags-input";

Vue.use(BootstrapVue);

import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";

export default {
  name: "Tags",

  //   props: ["userData"],
  components: {
    VueTagsInput,
  },
  data() {
    return {
      message: "",
      selectedUser: "",

      users: [
        { id: 1, value: "pankaj" },
        { id: 2, value: "manish" },
        { id: 3, value: "jayesh" },
      ],
      isSubmitted: false,
      tag: "",
      tags: [],
      autocompleteItems: [
        {
          text: "pankaj",
        },
        {
          text: "manish",
        },
        {
          text: "jayesh",
        },
      ],
    };
  },
  methods: {
    submitted() {
      //   alert("Data has been saved ");
      const tagarr = [];
      this.isSubmitted = true;
      this.tags.forEach((e) => {
        tagarr.push(e.text);
      });
      const formData = {
        id: Date.now(),
        message: this.message,
        user: this.selectedUser,
        tags: tagarr,
      };
      if (localStorage.getItem("data")) {
        const dataArr = JSON.parse(localStorage.getItem("data"));
        console.log(dataArr);
        dataArr.push(formData);

        localStorage.setItem("data", JSON.stringify(dataArr));
      } else {
        const formArray = [];
        formArray.push(formData);
        localStorage.setItem("data", JSON.stringify(formArray));
      }
      this.isSubmitted = false;
    },
  },
  computed: {
    filteredItems() {
      return this.autocompleteItems.filter((i) => {
        return i.text.toLowerCase().indexOf(this.tag.toLowerCase()) !== -1;
      });
    },
  },
};
</script>

<style scoped>
.heading {
  text-align: center;
  padding-bottom: 10px;
}
.main-section {
  padding: 47px 50px;
  height: 100%;
}
.form-section {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  border-radius: 5px;
  padding: 50px 70px;
  border: 1px solid #d6d1d1;
}
</style>