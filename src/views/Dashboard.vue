<template>
  <div>
    <Navbar :isLogged="true" />
    <div class="dashboard-container">
      <aside>
        <SearchInput class="search-input" />

        <div class="subjects">
          <ul>
            <li v-for="subject in subjects" v-bind:key="subject.id">
              {{ subject.name }}
            </li>
          </ul>
        </div>
      </aside>
      <main></main>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import SearchInput from "@/components/SearchInput.vue";
export default {
  components: {
    Navbar,
    SearchInput,
  },
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
};
</script>

<style scoped>
.dashboard-container {
  display: flex;
  width: 100%;
  height: 100vh;
}

aside {
  display: flex;
  flex-direction: column;
  border-right: 1px solid;
  width: 20%;
}

.search-input {
  margin-top: 30px;
  width: 70%;
  align-self: center;
}
.subjects ul {
  list-style: none;
}
.subjects ul li {
  display: flex;
  justify-content: center;
  padding: 10px 0;
  border-bottom: 1px solid;
}
.subjects ul li:first-child {
  border-top: 1px solid;
}
</style>
