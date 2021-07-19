<template>
  <div class="container">
    <navbar class="nav-bar" />

    <main>
      <div class="signup-container">
        <form v-on:submit.prevent="submitSignupForm">
          <input type="text" placeholder="nome" v-model="name" />
          <input type="text" placeholder="nome de usuário" v-model="username" />
          <input type="text" placeholder="email" v-model="email" />
          <input type="password" placeholder="senha" v-model="password" />
          <input
            type="password"
            placeholder="confirmar senha"
            v-model="confirmPassword"
          />

          <button class="submit-button" type="submit">resgistrar</button>
        </form>

        <router-link class="links" to="/login">
          <p>já tem conta? entre aqui</p>
        </router-link>
      </div>
    </main>
  </div>
</template>

<script>
import navbar from "@/components/Navbar.vue";

export default {
  components: {
    navbar,
  },
  data: () => ({
    name: "",
    username: "",
    email: "",
    password: "",
    confirmPassword: "",
  }),
  methods: {
    async submitSignupForm() {
      const { name, username, email, password, confirmPassword } = this;

      if (password !== confirmPassword) {
        alert("Senha e confirmação de senha estão diferentes!");
        return;
      }

      const body = {
        name,
        username,
        email,
        password,
      };

      const response = await fetch("http://localhost:3000/users", {
        method: "POST",
        body: JSON.stringify(body),
        headers: {
          Accept: "application/json",
          "Content-Type": "application/json",
        },
      });

      const jsonResponse = await response.json();

      if (response.status === 404 || response.status === 400) {
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

.signup-container {
  display: flex;
  flex-direction: column;
  width: 60%;
  margin-top: 10%;
  justify-content: center;

  height: 400px;
  align-items: center;
  background: #e0e0e0;
}

.signup-container form {
  display: flex;
  flex-direction: column;
  width: 60%;
}

.signup-container form input {
  width: 100%;
  height: 40px;
  margin-bottom: 20px;
  outline: none;
  padding: 10px;
}

.signup-container form button {
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

.submit-button:hover {
  background: #aaaaaa;
}
</style>
