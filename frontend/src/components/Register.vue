<template>
  <div class="row mt-3">
    <div class="col-md-2"></div>
    <div class="col-md-8">
      <form>
        <h2 class="text-center mb-3">Créer un Compte</h2>
          <div class="form-group">
            <label for="username">Utilisateur</label>
            <input id="username" v-model="username" name="username" type="text" class="form-control"/>
          </div>
          <div class="form-group">
            <label for="email">Adresse e-mail</label>
            <input id="email" v-model="email" name="email" type="email" class="form-control"/>
          </div>
          <div class="form-group">
            <label for="password">Mot de passe</label>
            <input id="password" v-model="password" name="password" type="password" class="form-control"/>
          </div>
          <div class="form-group">
              <div class="formSubmit"><a class="submit" href="#" v-on:click="handleRegister">Créer</a></div>
          </div>
      </form>
    </div>
    <div class="col-md-2"></div>
  </div>
</template>

<script>

export default {
  name: "Register",
  data() {
    return {
      username: "",
      email: "",
      password: "",
    };
  },
  computed: {
    loggedIn() {
      return this.$store.state.auth.status.loggedIn;
    },
  },
  mounted() {
    if (this.loggedIn) {
      this.$router.push("/profile");
    }
  },
  methods: {
    handleRegister(user) {
      user.username = this.username;
      user.email = this.email;
      user.password = this.password;


      this.$store.dispatch("auth/register", user).then(
        () => {
      this.username = user.username;
      this.email = user.email;
      this.password = user.password;
        },
      );
    this.$router.push("/login");
    },

  },
};
</script>

<style scoped>
</style>