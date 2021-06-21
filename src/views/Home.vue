<template>
  <div id="home-page">
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

    <main>
      <div class="main-container">
        <input type="text" class="home-search-input" placeholder="Pesquisar" />
        <div>
          <div
            class="subject-container"
            v-for="subject in subjects"
            v-bind:key="subject.id"
          >
            <div class="subject-name">
              {{ subject.name }}
              <button v-on:click="toggleDisplayDescription(subject.id)">
                botao
              </button>
            </div>
            <div
              class="subject-description"
              :style="subjectDescriptionStyle(subject.displayDescription)"
            >
              {{ subject.description }}
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "Home",
  data: () => ({
    subjects: [
      {
        id: "1",
        name: "calculo 1",
        description: "Materia mais legal do mundo",
        displayDescription: false,
      },
      {
        id: "2",
        name: "introdução a programação",
        description: "Devagar",
        displayDescription: false,
      },
    ],
  }),
  methods: {
    toggleDisplayDescription(id) {
      const index = this.subjects.findIndex((subject) => {
        return subject.id == id;
      });
      this.subjects[index].displayDescription =
        !this.subjects[index].displayDescription;
    },
    subjectDescriptionStyle(displayDescription) {
      return {
        display: displayDescription ? "flex" : "none",
      };
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

#home-page {
  height: 100vh;
}

main {
  height: 100%;
  display: flex;
  justify-content: center;
}

.main-container {
  display: flex;
  flex-direction: column;
  width: 60%;
  margin-top: 30px;
}

.home-search-input {
  width: 100%;
  height: 40px;
  border: none;
  border-radius: 8px;
  outline: none;
  padding: 4px 20px;
  background: #aaaaaa;
  margin-bottom: 20px;
}

.home-search-input::placeholder {
  color: #000000;
}

.subject-name {
  justify-content: space-between;
  display: flex;
  align-items: center;
  width: 100%;
  height: 40px;
  border: none;
  border-radius: 8px 8px 0 0;
  outline: none;
  padding: 4px 20px;
  background: #aaaaaa;
}

.subject-description {
  justify-content: space-between;
  display: flex;
  align-items: center;
  width: 100%;
  height: 40px;
  border: none;
  border-radius: 0 0 8px 8px;
  outline: none;
  padding: 4px 20px;
  background: #cccccc;
}

.subject-container {
  margin-bottom: 20px;
}
</style>
