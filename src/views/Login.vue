<template>
  <v-container fluid fill-height>
    <v-layout align-center justify-center>
      <v-flex xs12 sm8 md4>
        <v-card class="elevation-12">
          <v-toolbar dark color="primary">
            <v-toolbar-title>Voting Login</v-toolbar-title>
            <v-spacer></v-spacer>
          </v-toolbar>
          <v-card-text class='text-colour'>
            Please login with your Pheme details
          </v-card-text>
          <v-card-text class="form-ovrd">
            <v-form ref="form">
              <v-text-field
                v-model="login"
                prepend-icon="person"
                name="login"
                label="Login"
                type="text"
              />
              <v-text-field
                v-model="password"
                prepend-icon="lock"
                name="password"
                label="Password"
                id="password"
                type="password"
              />
            </v-form>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="primary" @click="submit">Login</v-btn>
          </v-card-actions>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import axios from 'axios';

export default {
  data: () => ({
    login: '',
    password: '',
    drawer: null,
  }),
  props: {
    source: String,
  },

  methods: {
    submit() {
      if (this.$refs.form.validate()) {
        // Native form submission is not yet supported
        // https://auth.makeuwa.com/api/login
        axios.post(
          'https://auth.makeuwa.com/api/login', JSON.stringify({
            login: this.login,
            password: this.password,
            token: process.env.VUE_APP_PHEME,
          }),
          {
            // mode: 'cors',
            headers:
            { crossDomain: true },
            withCredentials: true,
            credentials: 'same-origin',
          },
        )
          .then(res => console.table(res))
          .catch(err => console.log(err));
      }
    },
  },

};
</script>

<style>

.form-ovrd {
  padding-top: 0px;
}

.text-colour {
  color: rgba(0,0,0,.46);
}
</style>
