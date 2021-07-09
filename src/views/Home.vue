<template>
  <div id="home-page">
    <Navbar />
    <main>
      <div class="main-container">
        <SearchInput />
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
import Navbar from "@/components/Navbar.vue";
import SearchInput from "@/components/SearchInput.vue";
export default {
  components: {
    Navbar,
    SearchInput,
  },
  name: "Home",
  data: () => ({
    subjects: [],
  }),
  async created() {
    const response = await fetch("http://localhost:3000/subjects");
    const subjects = await response.json();

    this.subjects = subjects.map(subject => ({
          ...subject,
          displayDescription: false
          }));
  },
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
