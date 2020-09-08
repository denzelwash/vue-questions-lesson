<template>
  <div class="container">
    <div v-if="!showTable">
      <question-block 
        :type="info[step].type" 
        :title="info[step].title" 
        :answers="info[step].answers"
        @inputclick="addResult($event)"/>
      <button class="btn btn-primary" 
        v-if="step <= maxStep" 
        :disabled="disabled" 
        @click="nextStep">
        {{btnText}}</button>
    </div>
    <div v-else>
      <h2>Итого</h2>
      <hr>
      <table class="table table-bordered">
        <tr>
          <th>Вопрос</th>
          <th>Ваш ответ</th>
        </tr>
        <tr
          v-for="(item, index) in info"
          :key="index">
          <td>{{ item.title }}</td>
          <td>{{ result[index] ? result[index].toString() : '' }}</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
  import QuestionBlock from '@/components/QuestionBlock.vue';

  export default {
    name: 'App',
    components: {
      QuestionBlock
    },
    data() {
      return {
        info: [{
            type: 'radio',
            title: 'Какой тег задаёт ссылку?',
            answers: [
              'a',
              'div',
              'span',
              'img'
            ]
          },
          {
            type: 'checkbox',
            title: 'Какие из  этих тегов строчные?',
            answers: [
              'a',
              'div',
              'span',
              'img'
            ]
          },
          {
            type: 'radio',
            title: 'Какие тэги используются для определения заголовков?',
            answers: [
              'h1-h6',
              'Header',
              'Heading',
            ]
          }
        ],
        step: 0,
        maxStep: null,
        showTable: false,
        result: []
      }
    },
    computed: {
      disabled() {
        return this.result[this.step] ? false : true
      },
      btnText() {
        return this.step !== this.maxStep ? 'следующий вопрос' : 'Результат'
      }
    },
    methods: {
      addResult($event) {
        this.$set(this.result, this.step, $event)
      },
      nextStep() {
        if (this.step < this.maxStep) {
          this.step++
        } else {
          this.showTable = true
        }
      }
    },
    created() {
      this.maxStep = this.info.length - 1
    }
  }
</script>

<style lang="scss">
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  table {
    margin: 2rem 0;
  }
  td,
  th {
    width: 50%;
    padding: 1rem 0;
  }
</style>