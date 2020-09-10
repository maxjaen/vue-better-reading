<template>
  <div class="home">
    <div class="input">
      <textarea v-model="insertedText" placeholder="Paste your text"></textarea>
      <div>
        <button v-on:click="processWords()">Start Reading</button>
      </div>
      <p v-if="inReading" class="word">{{ currentDisplayedWord }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  props: {
    insertedText: String,
    currentDisplayedWord: String,
    inReading: Boolean,
  },
  data: function() {
    return {
      text: this.insertedText,
      word: this.currentDisplayedWord,
    };
  },
  methods: {
    processWords: async function() {
      const second = 1000;
      const wordsPerSecond = 4;
      const wordsFromInsertion = this.insertedText.split(' ');

      this.inReading = true;

      while (wordsFromInsertion.length !== 0) {
        let nextWord = wordsFromInsertion.shift();

        if (nextWord.split('.').length > 1) {
          this.currentDisplayedWord = `${nextWord} <---`;
          await this.wait(500);
        } else {
          this.currentDisplayedWord = `${nextWord}`;
          await this.wait(second / wordsPerSecond);
        }
      }

      this.inReading = false;
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
