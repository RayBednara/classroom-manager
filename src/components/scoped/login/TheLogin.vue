<template>
  <v-container fluid fill-height>
    <v-layout align-center justify-center>
      <v-flex xs12 sm8 md4>
        <v-card class="elevation-12">
          <v-card-text>
            <v-form>
              <v-text-field
                v-model="email"
                prepend-icon="person"
                label="Login"
                type="text"
              ></v-text-field>
              <v-text-field
                v-model="password"
                prepend-icon="lock"
                label="Password"
                type="password"
              ></v-text-field>
              <v-alert value="invalidLogin" color="error" icon="warning"
                >Invalid Login</v-alert
              >
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
      password: "",
      invalidLogin: false
    };
  },
  methods: {
    submitLogin: async function() {
      try {
        const results = await auth.signInWithEmailAndPassword(
          this.email,
          this.password
        );
        // store token inside of localStorage
        localStorage.setItem(
          "classroom.user",
          JSON.stringify({
            id: results.user.uid,
            token: results.user.refreshToken
          })
        );

        this.$router.push({ path: "/dashboard" });

        console.info(results);
      } catch (e) {
        if (e.code === "auth/wrong-password") {
          this.invalidLogin = true;
        }
      }
    }
  }
};
</script>
