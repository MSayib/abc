<template>
  <div>
    <!-- <form @submit.prevent="add">
      <input type="hidden" v-model="form.id" />
      <input type="text" v-model="form.name" />
      <button type="submit" v-show="!updateSubmit">add</button>
      <button type="button" v-show="updateSubmit" @click="update(form)">Update</button>
    </form>-->
    <!-- <ul v-for="user in users" :key="user.id">
      <li>
        <span>{{user.name}}</span> &#160;
        <button @click="edit(user)">Edit</button> ||
        <button @click="del(user)">Delete</button>
      </li>
    </ul>-->
    <form>
      <input v-model="orang.name" name="name" placeholder="name" />
      <input v-model="orang.role" name="role" type="text" placeholder="jabatan" />
      <input v-model="orang.id" name="id" type="hidden" placeholder="idnya" />
      <button @click.prevent="kirim">kirim</button>
    </form>
    <v-simple-table>
      <template v-slot:default @refresh-dong="load">
        <thead>
          <tr>
            <th class="text-left">Name</th>
            <th class="text-left">Role</th>
            <th class="text-left">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="orang in accounts" :key="orang.id">
            <td>{{ orang.id }}</td>
            <td>{{ orang.name }}</td>
            <td>{{ orang.role }}</td>
            <nuxt-link :to="'/home/' + orang.id">Details</nuxt-link>|
            <button @click="hapus">Hapus</button>
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
    role: {
      type: String,
      default: ""
    }
  },
  data() {
    return {
      //form ini perlu diganti, ini kode lama
      form: {
        id: "",
        name: ""
      },
      orang: {},
      //sampe sini
      users: "",
      updateSubmit: false,

      accounts: [],
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
        const res = await Axios.get("http://localhost:3003/accounts");
        this.accounts = res.data;

        if (this.accounts.length === 0) {
          this.isEmpty = true;
        }
      } catch (err) {
        console.error(err);

        this.isError = true;
      }

      this.isLoading = false;
    },
    kirim() {
      //FUNGSI CREATE berhasil, lihat accounts pada m.json untuk lihat detail dan baca data() diatas
      this.$axios
        .post("http://localhost:3003/accounts", this.orang)
        .then(() => {
          this.$router.push("/home");
        });
    },
    hapus() {
      const setuju = confirm("Data akan dihapus secara permanen..");
      if (!setuju) {
        return;
      }
      const setuju2 = confirm("Apakah Anda yakin?");
      if (!setuju2) {
        return;
      }

      this.$axios
        .delete("http://localhost:3003/accounts/" + this.form.id)
        .then(() => {
          this.$emit("refresh-dong");
        });
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
      //   axios.post("http://localhost:3002/accounts/", this.form).then(res => {
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