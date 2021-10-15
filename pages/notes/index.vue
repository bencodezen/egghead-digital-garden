<script>
export default {
  async asyncData({ $content }) {
    const notes = await $content("notes")
      .sortBy("publishOn", "desc")
      .fetch();

    return {
      notes
    };
  },
  data: () => ({
    selectedTag: ""
  }),
  computed: {
    displayedNotes() {
      if (this.selectedTag) {
        return this.notes.filter(note => note.tags.includes(this.selectedTag));
      } else {
        return this.notes;
      }
    }
  }
};
</script>

<template>
  <main>
    <h1>My Notes</h1>
    <p v-show="selectedTag">
      Filtered by: {{ selectedTag }}
      <button @click="selectedTag = ''">Clear</button>
    </p>
    <ul>
      <li v-for="note in displayedNotes" :key="note.slug + note.createdAt">
        <h2>
          <nuxt-link :to="`/notes/${note.slug}`">{{ note.title }}</nuxt-link>
        </h2>
        <p>Publish on: {{ new Date(note.publishOn) }}</p>
        <ul>
          <li
            v-for="tag in note.tags"
            :key="note.slug + tag"
            @click="selectedTag = tag"
          >
            {{ tag }}
          </li>
        </ul>
      </li>
    </ul>
  </main>
</template>
