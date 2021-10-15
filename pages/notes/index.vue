<script>
export default {
  data: () => ({
    notes: []
  }),
  async created() {
    this.notes = await this.$content("notes").fetch();
  }
};
</script>

<template>
  <main>
    <h1>My Notes</h1>
    <ul>
      <li v-for="note in notes" :key="note.slug + note.createdAt">
        <h2>{{ note.slug }}</h2>
      </li>
    </ul>
  </main>
</template>
