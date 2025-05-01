<template>
  <v-toolbar></v-toolbar>
  <v-container>
    <v-row>
      <v-col>
        <v-card>
          <v-card-item>
            <label class="ma-6">email</label>
            <input type="email" class="border-md" v-modle="name" /><br />
            <span v-for="err in v$.$errors" :key="err.$uid">
              <span>{{ err.$message }}</span>
            </span>
          </v-card-item>
          <!-- <v-card-item>
            <label class="ma-6">name</label>
            <input type="text" class="border-md" :v-model="name" /><br />
            <span v-for="err in v$.name.$errors" :key="err.$uid">
              <span>{{ err.$message }}</span>
            </span>
          </v-card-item>
          <v-card-item>
            <label class="ma-6">email</label>
            <input type="email" class="border-md" /><br />
            <span v-for="err in v$.name.$errors" :key="err.$uid">
              <span>{{ err.$message }}</span>
            </span>
          </v-card-item>
          <v-card-item>
            <label class="ma-8">age</label>
            <input type="namber" class="border-md" v-model="age" /><br />
            <span v-for="err in v$.name.$errors" :key="err.$uid">
              <span>{{ err.$message }}</span>
            </span>
          </v-card-item>
          <v-card-item>
            <label class="ma-3">password</label>
            <input type="password" class="border-md" /><br />
            <span v-for="err in v$.name.$errors" :key="err.$uid">
              <span>{{ err.$message }}</span>
            </span>
          </v-card-item> -->
          <v-btn class="ma-10" @click="val">submit</v-btn>
        </v-card>
      </v-col>
      <v-col>
        <p v-for="error of v$.$errors" :key="error.$uid">
          <strong>{{ error.$validator }}</strong>
          <small> on property</small>
          <strong>{{ error.$property }}</strong>
          <small> says:</small>
          <strong>{{ error.$message }}</strong>
        </p>
      </v-col>
    </v-row>
  </v-container>
  <router-view />
</template>

<script>
// @ is an alias to /src
import useVuelidate from "@vuelidate/core";
import { required, minLength, maxLength, alpha } from "@vuelidate/validators";

export default {
  setup() {
    return { v$: useVuelidate() };
  },

  data() {
    return {
      name: "",
    };
  },
  validations() {
    return {
      name: {
        required,
        minLength: minLength(3),
        maxLength: maxLength(10),
        alpha,
      },
    };
  },
  methods: {
    async val() {
      await this.v$.name.$validate();
      console.log(this.v$.name.$errors);
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
