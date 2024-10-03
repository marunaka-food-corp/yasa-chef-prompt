<template>
  <div>
    <h1>やさシェフ / プロンプト作成補助</h1>
    <p>WIP</p>
    <div v-if="generatedPrompt">
      <h4>プロンプト</h4>
      <textarea v-model="generatedPrompt" readonly></textarea>
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
      generatedPrompt: 'aaaaa'
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

textarea {
  resize: vertical;
  width: 600px;
  height: 150px;
}
</style>
