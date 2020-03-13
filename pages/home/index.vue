<template>
  <div>
    <div class="my-2">
      <v-btn small outlined color="primary" @click="search">Search</v-btn>
      <v-text-field
        v-model="query"
        label="Search"
        append-icon="mdi-magnify"
      ></v-text-field>
    </div>
    <nuxt-link to="/home/create">
      <v-btn class="mx-2" fab dark color="green">
        <v-icon dark>mdi-account-plus</v-icon>
      </v-btn>
    </nuxt-link>
    <!-- content -->
    <p v-if="isError">Error</p>
    <p v-else-if="isEmpty">Not Found</p>
    <v-simple-table v-else-if="!isLoading" class="mx-auto">
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-center">ID</th>
            <th class="text-center">Judul</th>
            <th class="text-center">Isi</th>
            <th class="text-center">Action</th>
          </tr>
        </thead>
        <ListItem
          v-for="post in posts"
          :id="post.id"
          :key="post.id"
          :judul="post.judul"
          :isi="post.isi"
          @refresh-ah="getData"
        >
        </ListItem>
      </template>
    </v-simple-table>
    <v-progress-circular
      v-else
      indeterminate
      color="primary"
    ></v-progress-circular>
    <!-- end-content -->
  </div>
</template>

<script>
import ListItem from "~/components/list.vue";
export default {
  components: { ListItem },
  data() {
    return {
      posts: [],
      isError: false,
      isEmpty: false,
      isLoading: false,
      query: ""
    };
  },
  mounted() {
    this.getData();
  },

  methods: {
    async search() {
      this.isLoading = true;

      try {
        const res = await this.$axios.get("http://localhost:3002/posts", {
          params: {
            q: this.query
          }
        });
        this.posts = res.data;

        if (this.posts.length === 0) {
          this.isEmpty = true;
        }
      } catch (err) {
        this.isError = true;
      }
      this.isLoading = false;
    },
    async getData() {
      this.isLoading = true;

      try {
        const res = await this.$axios.get("http://localhost:3002/posts");
        this.posts = res.data;

        if (this.posts.length === 0) {
          this.isEmpty = true;
        }
      } catch (err) {
        console.error(err);

        this.isError = true;
      }

      this.isLoading = false;
    }
  },
  computed: {
    filteredPosts: function() {
      return this.posts.filter(post => {
        return post.title.match(this.search);
      });
    }
  }
};
</script>

<style lang="css" scoped>
.spin {
  width: 5rem;
  height: 5rem;
  margin: 0 auto;
  position: fixed;
  top: 50%;
  left: 47%;
}
</style>
