<template>
  <div class="container">
    <Navbar class="nav-bar" />

    <main>
      <div class="login-container">
        <form>
          <input type="text" />
          <input type="text" />

          <button>Entrar</button>
        </form>

        <router-link to="/">
          <p>Não tem conta? Cadastre-se aqui</p>
        </router-link>
        <router-link to="/">
          <p>Esqueci minha senha</p>
        </router-link>
      </div>
    </main>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";

export default {
  components: {
    Navbar,
  },
};
</script>

<style>
main {
  display: flex;
  justify-content: center; /* justify-content no row eh para horizontal e align-items para vertical */
  height: 93%;
}

.login-container {
  display: flex;
  flex-direction: column;
  width: 60%;
  margin-top: 10%;

  height: 400px;
  align-items: center;
  background: #aaa;
}

.login-container form {
  display: flex;
  flex-direction: column;
}

.container {
  height: 100vh;
}

.nav-bar {
  height: 7%;
}
</style>
