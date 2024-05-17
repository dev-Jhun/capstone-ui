<template>
  <v-container fluid>
    <v-row justify="center" align="center" style="height: 100vh">
      <v-col cols="12" sm="8" md="4">
        <v-card class="mt-5" style="width: 500px; height: 350px" elevation="5" >
            <v-spacer></v-spacer> 
            <v-col>
              <v-card-title class="login-title">Login</v-card-title>
            </v-col>
            <v-spacer></v-spacer>
         

          <v-card-text>
            <v-form @submit.prevent="login">
              <v-text-field
                v-model="username"
                label="Username"
                outlined
              ></v-text-field>
              <v-text-field
                v-model="password"
                label="Password"
                outlined
                type="password"
              ></v-text-field>
              <v-btn type="submit" color="primary" block>Login</v-btn>
            </v-form>
            <!-- <div class="text-center mt-3">
              <router-link to="/registration"
                >Don't have an account? Register here</router-link
              >
            </div> -->
          </v-card-text>
        </v-card>
        <!-- <v-snackbar v-model="snackbar.show" :color="snackbar.color" :timeout="snackbar.timeout">{{ snackbar.message }}</v-snackbar> -->
      </v-col>
    </v-row>
    <!-- SUCCESS SNACKBAR     -->
    <v-snackbar color="green" v-model="successSnackbar">
      {{ textSuccess }}
      <template v-slot:action="{ attrs }">
        <v-btn
          plain
          color="white"
          v-bind="attrs"
          @click="successSnackbar = false"
        >
          Close
        </v-btn>
      </template>
    </v-snackbar>

    <!-- ERROR SNACKBAR     -->
    <v-snackbar color="red" v-model="errorSnackbar">
      {{ textError }}
      <template v-slot:action="{ attrs }">
        <v-btn color="white" text v-bind="attrs" @click="errorSnackbar = false">
          Close
        </v-btn>
      </template>
    </v-snackbar>
  </v-container>
</template>

<script>
import firebase from "~/plugins/firebase";

export default {
  layout: "login",
  data() {
    return {
      layout: "login",
      username: "",
      password: "",
      successSnackbar: false,
      errorSnackbar: false,
      textSuccess: "",
      textError: "",
    };
  },
  methods: {
    async login() {
      try {
        const snapshot = await firebase
          .database()
          .ref("UsernamePassword")
          .once("value");
        const userData = snapshot.val();

        if (
          userData.username === this.username &&
          userData.password === this.password
        ) {
          // Login successful
          // Redirect user to dashboard or another page
          this.$router.push("/dashboard");
          this.successSnackbar = true;
          this.textSuccess = "Succesfully Logged in";
        } else {
          // Username or password is incorrect
          console.error("Invalid username or password");
          this.errorSnackbar = true;
          this.textError = "Invalid username or password";
        }
      } catch (error) {
        // Handle login error
        console.error("Error logging in:", error.message);
        this.errorSnackbar = true;
        this.textError = "Invalid username or password";
      }
    },
  },
};
</script>

<style scoped>
.login-title {
  font-size: 24px;
  text-align: center;
  justify-content: center;
}
</style>
