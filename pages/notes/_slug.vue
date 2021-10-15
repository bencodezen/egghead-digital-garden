<script>
export default {
  async asyncData({ $content, route }) {
    const note = await $content(`notes/${route.params.slug}`).fetch();

    return {
      note
    };
  }
};
</script>

<template>
  <main>
    <h1>{{ note.title }}</h1>
    <nuxt-content :document="note" />
  </main>
</template>
