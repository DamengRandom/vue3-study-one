<template>
  <h3>{{word}}</h3>
  <p v-html="text"></p>
  <ul>
    <li v-bind:key="greeting.content" v-for="(greeting, index) in greetings">
      {{ index + 1 }} - {{ greeting.content }}
    </li>
  </ul>
  <!-- <button v-on:click="handleClick(2)">Click Me</button> -->
  <button @click="handleClick(2)">Click Me</button>
  <p>Show 2 way data binding text string: {{ textString }}</p>
  <!-- <input type="text" :value="textString" @input="handleChange($event)" /> -->
  <input type="text" v-model="textString" />
  <p>{{ keyupEnterString }}</p>
  <input type="text" :value="keyupEnterString" @keyup.enter="processKeyEnter($event)"/>
</template>

<script>
  export default {
    data() {
      return {
        word: 'Hi Vue',
        text: 'mate mate ..',
        greetings: [{content: 'whats up'}, {content:'how are you'}, {content:'hello'}, {content:'aloha'}],
        textString: '',
        keyupEnterString: []
      }
    },
    beforeCreate() {
      console.log('before created: ', this.word); // undefined
    },
    created() {
      console.log('created: ', this.word); // 'Hi Vue'
      this.word = 'after created(), go to beforeMount()'
    },
    beforeMount() {
      console.log('before mount: ', this.word); // 'Hi Vue'
    },
    mounted() {
      this.word = 'Vue allows "this" directly access variable "word", this is the magic part of Vue. Normally, we should do this.data().word, but Vue can directly put word as same level with data() function, so we can directly access as "this.word"'
      console.log(this.word);
    },
    methods: {
      handleClick(value) {
        this.hiVue();
        console.log('get value: ', value);
      },
      handleChange(event) {
        this.textString = event.target.value;
      },
      processKeyEnter(event) {
        this.keyupEnterString = event.target.value;
      },
      hiVue() {
        alert('Hi Vue ..');
      },
    }
  }
</script>

<style scoped>
  h3 {
    color: teal;
  }
</style>
