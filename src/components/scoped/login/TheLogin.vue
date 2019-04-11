<template>
  <v-container fluid fill-height>
    <v-layout align-center justify-center>
      <v-flex xs12 sm8 md4>
        <v-card class="elevation-12">
          <v-card-text>
            <v-form>
              <v-text-field v-model="email" prepend-icon="person" label="Login" type="text"></v-text-field>
              <v-text-field v-model="password" prepend-icon="lock" label="Password" type="password"></v-text-field>
            </v-form>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="primary" @click="submitLogin">Login</v-btn>
          </v-card-actions>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>



<script>
import { auth } from "@/services/firebase";

export default {
  data: () => {
    return {
      email: "",
      password: ""
    };
  },
  methods: {
    submitLogin: async function() {
      try {
        const results = await auth.signInWithEmailAndPassword(
          this.email,
          this.password
        );
      } catch (e) {
        console.log("got an error");
      }
    }
  }
};
</script>
