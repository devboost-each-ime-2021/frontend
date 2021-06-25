<template>
  <nav>
    <div class="nav-title">
      <h1>Cadê o link?</h1>
    </div>
    <div class="nav-options">
      <ul>
        <li v-if="!isLogged">
          <router-link to="/dashboard"> Entrar </router-link>
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
