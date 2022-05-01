<template>
  <div class="row mt-3">
    <div class="col-md-2"></div>
    <div class="col-md-8">
      <form>
        <p class="text-center mb-3">
          Vous n'avez pas de compte ?
          <a href="/register">Merci de vous inscrire ! </a>
        </p>
        <div class="form-group">
          <label for="username">Utilisateur</label>
          <input id="username" v-model="username" name="username" type="text" class="form-control"/>
        </div>
        <div class="form-group">
          <label for="password">Mot de passe</label>
          <input id="password" v-model="password" name="password" type="password" class="form-control"/>
        </div>

        <div class="form-group">
            <div class="formSubmit"><a class="submit" href="#" v-on:click="handleLogin">Connexion</a></div>
        </div>

      </form>
    </div>
    <div class="col-md-2"></div>
  </div>
</template>

<script>

export default {
  name: "Login",
  data() {
    return{
    username: "",
    password: ""
    }
  },
  computed: {
    loggedIn() {
      return this.$store.state.auth.status.loggedIn;
    },
  },
  created() {
    if (this.loggedIn) {
      this.$router.push("/profile");
    }
  },
  methods: {
    handleLogin(user) {
      console.log(user)
      user.username = this.username;
      user.password = this.password;

      this.$store.dispatch("auth/login", user).then(
        () => {
          this.$router.push("/profile");
        },
      );
    },
  },
};
</script>

<style scoped>
</style>