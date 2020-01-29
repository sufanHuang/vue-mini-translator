
<template>
  <div class = 'text-center' id="app">
    <h1>Mini Translator</h1>
    <h5>Powered by Vue.js</h5>
    <hr>
    <div class="row" >
      <form class="form-inline well"  @submit="formSubmit">
        <input class = 'form-control' type ='text' v-model="textToTranslate" placeholder="Enter a Word...">
        <select class="form-control" v-model="language">
          <option value = "ru">Russian</option>
          <option value = "zh">Chinese</option>
          <option value = "es">Spanish</option>
        </select>
        <hr>
        <input class="btn btn-primary" type ='submit' value="translate">
      </form>
    </div>
    <h2 class ='text-danger'> {{translatedText}} </h2>
  </div>
</template>

<script>
    import axios from 'axios'

    export default {
        name: 'App',
        data: function() {
            return{
                textToTranslate: '',
                language: '',
                translatedText: ''
            }
        },
        created(){
            this.language = 'zh'
        },
        methods: {
            translateText: function(text,language){
                axios.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20200122T212506Z.be34317ff507f6f7.b3adba3cf5ff64da7f708049efbe54529c11574d&lang='+language+'&text='+text)
                    .then((response)=>{
                        this.translatedText = response.data.text[0]
                        console.log(this.translatedText)
                    })
                    .catch(error => console.log(error))
            },
            formSubmit: function(e){
                this.translateText(this.textToTranslate,this.language)
                e.preventDefault()
            }
        }
    }
</script>

<style>
  body {
    background: darkslategray;
  }

</style>
