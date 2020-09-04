<template>
  <div class="home">
    <div class="input">
      <textarea v-model="insertedText" placeholder="Paste your text"></textarea>
      <div>
        <button v-on:click="processWords()">Display</button>
      </div>
      <p class="word">{{ currentDisplayedWord }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  props: {
    insertedText: String,
    currentDisplayedWord: String,
  },
  data: function() {
    return {
      text: this.insertedText,
      word: this.currentDisplayedWord,
    };
  },
  methods: {
    processWords: async function() {
      const wordsFromInsertion = this.insertedText.split(' ');

      while (wordsFromInsertion.length !== 0) {
        this.currentDisplayedWord = wordsFromInsertion.shift();
        await this.wait(300);
      }
    },
    wait: async function(milliseconds) {
      return new Promise((resolve) => setTimeout(resolve, milliseconds));
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.home {
  height: 100vh;
  min-width: 300px;
  background-color: #7e9389;
  padding: 70px;
}

.word {
  white-space: pre-line;
  text-align: center;
  font-size: 50px;
}

textarea {
  height: 250px;
  width: -moz-available;
}
</style>
