<template>
  <div>
    <v-layout column justify-center align-center>
      <v-flex xs12 sm8 md6>
        <div class="text-center">
          <logo />
          <vuetify-logo />
        </div>
        <v-card>
          <v-card-title class="headline">
            Welcome ..
          </v-card-title>
          <v-card-text>
            Just.. hello..
            <div class="text-xs-right">
              <em><small>&mdash; M Sayib & Farhan</small></em>
            </div>
            <hr class="my-3" />
            <a href="https://instagram.com/sybrzq/" target="_blank">
              @sybrzq
            </a>
            <br />
            <a href="https://instagram.com/" target="_blank"> Farhan </a>
          </v-card-text>
          <v-card-actions>
            <v-spacer />
            <v-btn color="primary" nuxt to="/front">
              Front
            </v-btn>
            <v-btn color="success" nuxt to="/login">
              Login
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
import Logo from "~/components/Logo.vue";
import VuetifyLogo from "~/components/VuetifyLogo.vue";

export default {
  components: {
    Logo,
    VuetifyLogo
  }
};
</script>
