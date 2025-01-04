<template>
  <div>
    <h1>やさシェフ / プロンプト作成補助</h1>
    <form @submit.prevent="generate">
      <div>
        <label for="ingredients">食材：&nbsp;</label>
        <input v-model="item.ingredients" id="ingredients" placeholder="任意" />
      </div>
      <div>
        <label for="allergies">アレルギー:&nbsp;</label>
        <input v-model="item.allergies" id="allergies" placeholder="任意" />
      </div>
      <div>
        <label for="cookTime">調理時間(分):&nbsp;</label>
        <input type="number" v-model.number="item.cookTime" id="cookTime" placeholder="任意" />
      </div>
      <div>
        <label for="season">季節:&nbsp;</label>
        <select v-model="item.season">
          <option value="">季節を選択</option>
          <option value="春">春</option>
          <option value="夏">夏</option>
          <option value="秋">秋</option>
          <option value="冬">冬</option>
        </select>
      </div>
      <button type="submit">プロンプト作成</button>
    </form>
    <div v-if="generatedPrompt" class="generated-prompt">
      <textarea v-model="generatedPrompt" readonly></textarea>
      <br />
      <button @click="copy" style="margin-right: 10px;">コピー</button>
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
      if (this.item.ingredients) {
        prompt += `${this.item.ingredients}を使用してください。\n`
      } else {
        prompt += '食材の指定はありません。\n'
      }

      this.generatedPrompt = prompt
    },
    copy() {
      navigator.clipboard.writeText(this.generatedPrompt)
    },
    clear() {
      this.item.ingredients = ''
      this.generatedPrompt = ''
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
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
