<template>
  <div>
    <Navbar :isLogged="true" />
    <div class="dashboard-container">
      <aside>
        <SearchInput class="search-input" />

        <div class="subjects">
          <ul>
            <li
              v-for="(subject, index) in subjects"
              v-bind:key="subject.id"
              @click="changeSubject(index)"
              :id="currentSubjectStyle(index)"
            >
              {{ subject.name }}
            </li>
          </ul>
        </div>
      </aside>
      <main>
        <SubjectContent :subject="subjects[currentSubject]" />
      </main>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import SearchInput from "@/components/SearchInput.vue";
import SubjectContent from "@/components/SubjectContent.vue";

export default {
  components: {
    Navbar,
    SearchInput,
    SubjectContent,
  },
  data: () => ({
    currentSubject: 0,
    subjects: [
      {
        id: "1",
        name: "calculo 1",
        description: "Materia mais legal do mundo",
        sections: [
          {
            id: "1",
            title: "Derivada",
            items: [
              { id: "1", title: "cosseno" },
              { id: "2", title: "seno" },
              { id: "3", title: "tangente" },
            ],
          },
          {
            id: "2",
            title: "Limites",
            items: [
              { id: "1", title: "cosseno" },
              { id: "2", title: "seno" },
              { id: "3", title: "tangente" },
            ],
          },
        ],
      },
      {
        id: "2",
        name: "introdução a programação",
        description: "Devagar",
        sections: [
          {
            id: "1",
            title: "Ponteiros",
            items: [
              { id: "1", title: "cosseno" },
              { id: "2", title: "seno" },
              { id: "3", title: "tangente" },
            ],
          },
        ],
      },
    ],
  }),
  methods: {
    changeSubject(index) {
      this.currentSubject = index;
    },
  },
  computed: {
    currentSubjectStyle() {
      return (index) => {
        return this.currentSubject === index ? "item-clicked" : "";
      };
    },
  },
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

main {
  width: 80%;
}

.search-input {
  margin-top: 30px;
  width: 70%;
  align-self: center;
}

.subjects ul {
  list-style: none;
}

#item-clicked {
  background: #AAA;
}

.subjects ul li {
  display: flex;
  justify-content: center;
  padding: 10px 0;
  border-bottom: 1px solid;
  cursor: pointer;
}

.subjects ul li:hover {
  background: #ddd;
}

.subjects ul li:first-child {
  border-top: 1px solid;
}
</style>
