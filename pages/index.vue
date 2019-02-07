<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <h1>Search iTunes</h1>
      <br>

      <v-form v-model="valid" @submit.prevent="submit">
        <v-text-field label="Artist Name" v-model="artName" :rules="nameRules" required></v-text-field>
      </v-form>
    </v-flex>
  </v-layout>
</template>

<script>
// import Logo from '~/components/Logo.vue'

export default {
  components: {},
  data() {
    return {
      valid: false,
      artName: "",
      nameRules: [
        v => !!v || "Name is required",
        v => v.length <= 15 || "Name must be less than 15 characters"
      ]
    };
  },
  methods: {
    submit(event) {
      // alert("Hello world");
      this.$router.push(`results/${this.artName}`);
    }
  }
};
</script>
