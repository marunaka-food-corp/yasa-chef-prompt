<template>
  <div id="app">
    <h1>やさシェフ / プロンプト作成補助</h1>
    <form @submit.prevent="generate" class="card">
      <div class="form-group">
        <label for="ingredients">食材:</label>
        <input v-model="item.ingredients" id="ingredients" placeholder="任意" />
      </div>
      <div class="form-group">
        <label for="allergies">アレルギー:</label>
        <input v-model="item.allergies" id="allergies" placeholder="任意" />
      </div>
      <div class="form-group">
        <label for="cookTime">調理時間 (min):</label>
        <input type="number" v-model.number="item.cookTime" id="cookTime" placeholder="任意" />
      </div>
      <div class="form-group">
        <label for="season">季節:</label>
        <select v-model="item.season">
          <option value="">季節を選択</option>
          <option value="春">春</option>
          <option value="夏">夏</option>
          <option value="秋">秋</option>
          <option value="冬">冬</option>
        </select>
      </div>
      <div class="button-row">
        <button type="submit" class="primary">プロンプト作成</button>
        <button type="button" @click="inputSampleData">サンプルデータを入力</button>
      </div>
    </form>
    <div v-if="generatedPrompt" class="generated-prompt">
      <textarea v-model="generatedPrompt" readonly></textarea>
      <div class="button-row">
        <button @click="copy" class="primary">コピー</button>
        <button @click="clear">クリア</button>
      </div>
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
        allergies: '',
        cookTime: null,
        season: '',
      },
      generatedPrompt: ''
    }
  },
  methods: {
    generate() {
      let prompt = '高齢者施設向けの献立を提案してください。\n\n'

      // 食材
      if (this.item.ingredients) {
        prompt += `・${this.item.ingredients}をメインの食材として使用してください\n`
      } else {
        prompt += '・食材の指定はありません\n'
      }

      // アレルギー
      if (this.item.allergies) {
        prompt += `・アレルギーのため、${this.item.allergies}を使用しないでください\n`
      }

      // 調理時間
      if (this.item.cookTime) {
        prompt += `・調理時間は、${this.item.cookTime}分以内を想定してください\n`
      }

      // 季節
      if (this.item.season) {
        prompt += `・喫食する季節として、${this.item.season}を想定してください\n`
      }

      this.generatedPrompt = prompt
    },
    inputSampleData() {
      this.item.ingredients = '鶏肉'
      this.item.allergies = '乳製品'
      this.item.cookTime = 20
      this.item.season = '冬'
    },
    copy() {
      navigator.clipboard.writeText(this.generatedPrompt)
    },
    clear() {
      this.item.ingredients = ''
      this.item.allergies = ''
      this.item.cookTime = null
      this.item.season = ''
      this.generatedPrompt = ''
    }
  }
}
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: left;
  color: #2c3e50;
  margin: 30px auto;
  max-width: 700px;
}

h1 {
  font-size: 1.8rem;
  margin-bottom: 1.5rem;
}

.card {
  background-color: #f9f9f9;
  padding: 1.5rem;
  border: 1px solid #ddd;
  border-radius: 8px;
}

.form-group {
  display: flex;
  align-items: center;
  margin-bottom: 1rem;
}

.form-group label {
  width: 130px;
  font-weight: bold;
  margin-right: 10px;
}

.form-group input,
.form-group select {
  flex: 1;
  padding: 0.5rem;
  font-size: 1rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.button-row {
  display: flex;
  gap: 10px;
  margin-top: 1rem;
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
