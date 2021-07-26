<template>
  <div class="subject-container">
    <div class="subject-title">
      <h1>{{ subject.name }}</h1>
    </div>
    <SubjectSection
      v-for="section in subject.sections"
      v-bind:key="section._id"
      :section="section"
    />
  </div>
</template>

<script>
import SubjectSection from "@/components/SubjectSection.vue";

export default {
  components: {
    SubjectSection,
  },
  props: {
    subject: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style>
.subject-container {
  display: flex;
  flex-direction: column;
  padding: 30px;
  width: 100%;
}

.subject-title {
  width: 100%;
  padding: 10px;
  background: #aaaaaa;
}
</style>
