<template>
  <div class="container">
    <Navbar class="nav-bar" />

    <main>
      <div class="login-container">
        <form v-on:submit.prevent="submitLoginForm">
          <input
            type="text"
            placeholder="Nome de usuário ou email"
            v-model="user"
          />
          <input type="password" placeholder="Senha" v-model="password" />

          <button type="submit">Entrar</button>
        </form>

        <router-link class="links" to="/">
          <p>Não tem conta? Cadastre-se aqui</p>
        </router-link>
        <router-link class="links" to="/">
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
  data: () => ({
    user: "",
    password: "",
  }),
  methods: {
    async submitLoginForm() {
      const body = {
        user: this.user,
        password: this.password,
      };

      console.table(body);

      const response = await fetch("http://localhost:3000/login", {
        method: "POST",
        body: JSON.stringify(body),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Accept: "application/json",
        },
      });

      const jsonResponse = await response.json();

      if (response.status === 404) {
        alert(jsonResponse.message);
      } else {
        const userID = jsonResponse.id;
        this.$router.push({
          name: "Dashboard",
          params: {
            id: userID,
          },
        });
      }
    },
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
  justify-content: center;

  height: 400px;
  align-items: center;
  background: #e0e0e0;
}

.login-container form {
  display: flex;
  flex-direction: column;
  width: 60%;
}

.login-container form input {
  width: 100%;
  height: 40px;
  margin-bottom: 20px;
  outline: none;
  padding: 10px;
}

.login-container form button {
  margin-bottom: 24px;
  padding: 10px;
  background: #c4c4c4;
  border: none;
  font-size: 20px;
}

.links {
  text-decoration: none;
  color: #000;
  margin-bottom: 10px;
}

.container {
  height: 100vh;
}

.nav-bar {
  height: 7%;
}
</style>
