<template>
  <div>
    <h1>やさシェフ / プロンプト作成補助</h1>
    <form @submit.prevent="generate">
      <div>
        <label for="ingredients">食材を指定する：&nbsp;</label>
        <input v-model="item.ingredients" id="ingredients" placeholder="任意" />
      </div>
      <button type="submit">プロンプト作成</button>
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
      let p = '高齢者施設向けの献立を提案してください。'
      this.generatedPrompt = p
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
  text-align: left;
  color: #2c3e50;
  margin-top: 30px;
  margin-left: 60px;
}

.generated-prompt {
  margin-top: 60px;
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
