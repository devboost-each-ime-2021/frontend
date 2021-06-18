<template>
  <div>
    <nav>
      <div class="nav-title">
        <h1>Cadê o link?</h1>
      </div>
      <div class="nav-options">
        <ul>
          <li>Entrar</li>
          <li>Cadastrar</li>
          <li>Sobre</li>
        </ul>
      </div>
    </nav>

    <div class="home">Welcome!</div>
  </div>
</template>

<script>
export default {
  name: "Home",
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
