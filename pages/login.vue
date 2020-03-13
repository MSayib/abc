<template>
<v-app id="login">
  <v-content>
    <v-container>
      <body class="text-center">
        <v-card class="elevation-12">
          <v-toolbar color="primary" dark flat>
            <v-toolbar-title>Masuk</v-toolbar-title>
            <v-spacer />
            <!-- <v-tooltip right> // buat nambah icon + fungsi tombol link keluar di pojok atas Login Form
                  <template v-slot:activator="{ on }">
                    <v-btn
                      icon
                      large
                      href="https://codepen.io/johnjleider/pen/pMvGQO"
                      target="_blank"
                      v-on="on"
                    >
                      <v-icon>mdi-codepen</v-icon>
                    </v-btn>
                  </template>
                  <span>Codepen</span>
            </v-tooltip>-->
          </v-toolbar>
          <v-card-text>
            <v-form>
              <v-text-field
                label="Username"
                name="username"
                prepend-icon="mdi-account"
                type="text"
              />
              <!-- nyari kode icon disini : https://materialdesignicons.com/cdn/2.0.46/ -->
              <v-text-field
                id="password"
                label="Password"
                name="password"
                prepend-icon="mdi-lock"
                type="password"
              />
            </v-form>
          </v-card-text>
          <v-card-actions>
            <v-spacer />
            <v-btn color="primary" nuxt to="/home">Login</v-btn>
          </v-card-actions>
        </v-card>
      </body>
    </v-container>
  </v-content>
</v-app>
</template>

<script>
export default {
  props: {
    source: String
  }
};
</script>