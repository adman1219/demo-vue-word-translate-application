<template>
  <div class="text-center" id="app">
    <h1>Word Translator</h1>
    <h5>Powered By Vue.js</h5>
    <TranslateForm v-on:formSubmit="translateText"></TranslateForm>
    <TranslateOutput v-text="translatedText"></TranslateOutput>
  </div>
</template>

<script>
  import TranslateForm from './components/TranslateForm'
  import TranslateOutput from './components/TranslateOutput'
  export default {
    name: 'App',
    components: {
      TranslateForm,
      TranslateOutput
    },
    data: function () {
      return {
        translatedText: ''
      }
    },
    methods: {
      translateText: function (text, language) {
        const key = 'trnsl.1.1.20181109T053506Z.a763ac38b5fb5490.626836616547322a7f723c9eaae2ae64567ed8ed';
        this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key='
          + key + '&text=' + text +'&lang=' + language)
          .then((req) => {
            this.translatedText = req.body.text[0];
          });
      }
    }
  }
</script>

<style>
  body {
    background: #fefefe;
  }
</style>
