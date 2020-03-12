<template>
  <div>
    <form @submit.prevent="add">
      <input type="hidden" v-model="form.id" />
      <input type="text" v-model="form.name" />
      <button type="submit" v-show="!updateSubmit">add</button>
      <button type="button" v-show="updateSubmit" @click="update(form)">Update</button>
    </form>
    <ul v-for="user in users" :key="user.id">
      <li>
        <span>{{user.name}}</span> &#160;
        <button @click="edit(user)">Edit</button> ||
        <button @click="del(user)">Delete</button>
      </li>
    </ul>
    <v-simple-table>
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left">Name</th>
            <th class="text-left">Calories</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="dessert in desserts" :key="dessert.name">
            <td>{{ dessert.name }}</td>
            <td>{{ dessert.calories }}</td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </div>
  <!-- ini crud sederhana yg udah work tinggal modif dikasih style -->
</template>

<script>
/* eslint-disable */
/* kalo eslint keinstall di project atau di vscode lu, aktifin eslint-disable disini */
/* imprt Axios < hurufnya case sensitive, wajib import klo pake code dibawah ini, kecuali 
sebelumnya udah pernah install axios dari nuxt pas install project bisa panggil axios tapi huruf kecil*/

import Axios from "axios";
// props disini difungsikan buat bikin variabel yg bisa dipanggil ke table vuetify dan datanya bisa dipanggil lewat array dari API jsons-server
export default {
  props: {
    name: {
      type: String,
      default: ""
    },
    calories: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      form: {
        id: "",
        name: ""
      },
      users: "",
      updateSubmit: false,

      desserts: [],
      isError: false,
      isEmpty: false,
      isLoading: false,
      cari: ""
    };
  },
  mounted() {
    this.load();
  },
  methods: {
    async load() {
      this.isLoading = true;

      try {
        const res = await Axios.get("http://localhost:3003/desserts");
        this.desserts = res.data;

        if (this.desserts.length === 0) {
          this.isEmpty = true;
        }
      } catch (err) {
        console.error(err);

        this.isError = true;
      }

      this.isLoading = false;
      // load() {
      //   axios
      //     .get("http://localhost:3002/users")
      //     .then(res => {
      //       this.users = res.data;
      //     })
      //     .catch(err => {
      //       console.log(err);
      //     });
      // },
      // add() {
      //   axios.post("http://localhost:3002/users/", this.form).then(res => {
      //     this.load();
      //     this.form.name = "";
      //   });
      // },
      // edit(user) {
      //   this.updateSubmit = true;
      //   this.form.id = user.id;
      //   this.form.name = user.name;
      // },
      // update(form) {
      //   return axios
      //     .put("http://localhost:3002/users/" + form.id, { name: this.form.name })
      //     .then(res => {
      //       this.load();
      //       this.form.id = "";
      //       this.form.name = "";
      //       this.updateSubmit = false;
      //     })
      //     .catch(err => {
      //       console.log(err);
      //     });
      // },
      // del(user) {
      //   axios.delete("http://localhost:3002/users/" + user.id).then(res => {
      //     this.load();
      //     let index = this.users.indexOf(form.name);
      //     this.users.splice(index, 1);
      //   });
    }
  }
};
</script>