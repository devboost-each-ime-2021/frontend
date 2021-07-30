<template>
  <div id="home-page">
    <Navbar />
    <main>
      <div class="main-container">
        <SearchInput v-on:onSearchChange="filterData" />
        <div>
          <div
            class="subject-container"
            v-for="subject in displaySubjects"
            v-bind:key="subject._id"
          >
            <div class="subject-name">
              {{ subject.name }}
              <button v-on:click="toggleDisplayDescription(subject._id)">
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
import SearchInput from "@/components/SearchInput.vue";
import Navbar from "@/components/Navbar.vue";
export default {
  components: {
    Navbar,
    SearchInput,
  },
  name: "Home",
  data: () => ({
    subjects: [],
    filteredSubjects: undefined,
  }),
  async created() {
    const response = await fetch("http://localhost:3000/subjects");
    const subjects = await response.json();

    this.subjects = subjects.map((subject) => ({
      ...subject,
      displayDescription: false,
    }));
    console.log(subjects);
  },
  computed: {
    displaySubjects() {
      return this.filteredSubjects === undefined
        ? this.subjects
        : this.filteredSubjects;
    },
  },
  methods: {
    filterData(text) {
      const filteredSubjects = this.subjects.filter((subject) => {
        const keys = Object.keys(subject);
        return keys.some((key) => {
          if (key === "displayDescription") {
            return false;
          } else if (key === "sections") {
            return subject[key].some((section) => {
              return (
                this.compareStrings(section.title, text) ||
                section.items.some((item) => {
                  return this.compareStrings(item.title, text);
                })
              );
            });
          }
          return this.compareStrings(subject[key], text);
        });
      });
      this.filteredSubjects = filteredSubjects;
    },
    compareStrings(s1, s2) {
      return s1.toLowerCase().includes(s2.toLowerCase());
    },
    toggleDisplayDescription(id) {
      const index = this.subjects.findIndex((subject) => {
        return subject._id == id;
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
