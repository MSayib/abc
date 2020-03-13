<template>
  <v-app>

  <v-toolbar
    :flat="true"
    app
    fixed
    clipped-left
    color="#000000"
    dark>
    <v-toolbar-title class="pointer">
      <router-link
        to="/"
        class="pointer"
        tag="h1">
        Blog
      </router-link>
    </v-toolbar-title>
    <v-spacer/>
    <v-toolbar-items>
      <v-btn
        flat
        nuxt
        to="/posts">
        <v-icon
          dark
          left></v-icon>
        Blog
      </v-btn>
      <v-btn
        flat
        nuxt
        to="/admin">
        <v-icon
          dark
          left></v-icon>
        Admin
      </v-btn>
    </v-toolbar-items>
  </v-toolbar>

    <v-content> <nuxt /> </v-content>

    <v-footer dark>
      <v-container class="d-flex grey--text text--darken-1 font-weight-medium">
        <span>Farhan Dan Sayib &copy; 2020</span> <v-spacer />
        <span> Tetamba Studio Kreasi </span>
      </v-container>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'Navigation'
}
</script>

<style scoped>
.pointer {
  cursor: pointer;
}
</style>
