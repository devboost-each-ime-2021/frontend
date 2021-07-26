<template>
  <section>
    <h2>{{ section.title }}</h2>
    <ul>
      <li v-for="item in section.items" v-bind:key="item.title">
        {{ item.title }}
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  props: {
    section: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style></style>
