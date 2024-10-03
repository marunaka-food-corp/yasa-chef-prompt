<template>
  <div>
    <h1>やさシェフ / プロンプト作成補助</h1>
    <form @submit.prevent="generate">
      <button type="submit">作成</button>
    </form>
    <div v-if="generatedPrompt" class="generated-prompt">
      <textarea v-model="generatedPrompt" readonly></textarea>
      <br />
      <button @click="clear">クリア</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      item: {
        ingredients: '',
      },
      generatedPrompt: ''
    }
  },
  methods: {
    generate() {
      this.generatedPrompt = `aaaaa`
    },
    clear() {
      this.generatedPrompt = ''
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.generated-prompt {
  margin-top: 100px;
}

button {
  margin-top: 10px;
}

textarea {
  resize: vertical;
  width: 600px;
  height: 150px;
}
</style>
