<template>
  <div class="container">
    <div v-if="error">
      {{ error }}
    </div>
    <ul v-else class="list">
      <h2>Вопросы по поводу вакансии</h2>
      <li v-for="item in items" :key="item.id">{{ item.name }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      items: [],
      error: null
    };
  },
  async mounted () {
    try {
      this.items = await this.$strapi.$items.find();
    } catch (error) {
      this.error = error;
    }
  }
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.list {
  display: flex;
  flex-direction: column;
  padding-left: 0;
  align-items: flex-start;
}
</style>
