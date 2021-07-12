<template>
  <nav>
    <div class="nav-title">
      <router-link class="home-page-button" to="/">
        <h1>Cadê o link?</h1>
      </router-link>
    </div>
    <div class="nav-options">
      <ul>
        <li v-if="!isLogged">
          <router-link to="/Login"> Entrar </router-link>
        </li>
        <li v-if="!isLogged">Cadastrar</li>
        <li>Sobre</li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  props: {
    isLogged: {
      type: Boolean,
      default: () => false,
    },
  },
};
</script>

<style scoped>
nav {
  display: flex;
  justify-content: space-between;
  background-color: #aaaaaa;
  padding: 20px;
}

.home-page-button {
  text-decoration: none;
  color: #000;
}

.nav-options ul {
  list-style: none;
  display: flex;
  height: 100%;
  align-items: center;
  justify-content: space-between;
}

.nav-options ul li {
  margin-right: 20px;
}
</style>
