<template>
  <div>
    <h2>{{title}}</h2>
    <hr>
    <div :ref="type === 'checkbox' ? 'checkboxBlock' : ''">
      <app-input
        v-for="(item, index) in answers"
        :key="index"
        :answer="item"
        :index="index"
        :type="type"
        @inputclick="onClick($event)"
      />
    </div>
  </div>
</template>

<script>
import AppInput from '@/components/AppInput.vue';

export default {
  name: 'QuestionBlock',
  components: {
    AppInput,
  },
  props: {
    title: String,
    type: String,
    answers: Array
  },
  data() {
    return {

    }
  },
  methods: {
    onClick(e) {
      const value = e.target.value
      if (this.type === 'radio') {
        this.$emit('inputclick', value)
      }
      if (this.type === 'checkbox') {
        let checkboxes = this.$refs.checkboxBlock.querySelectorAll('input:checked')
        checkboxes = Array.from(checkboxes).map(elem => {
          return elem.value ? elem.value : false
        })
        this.$emit('inputclick', checkboxes)
      }
    }
  }
}
</script>

<style>

</style>