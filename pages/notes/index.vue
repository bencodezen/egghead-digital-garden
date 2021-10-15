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
        <h2>{{ note.title }}</h2>
        <p>Publish on: {{ new Date(note.publishOn) }}</p>
        <ul>
          <li v-for="tag in note.tags" :key="note.slug + tag">
            {{ tag }}
          </li>
        </ul>
      </li>
    </ul>
  </main>
</template>
