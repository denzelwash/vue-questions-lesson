<template>
  <div class="form-group">
    <label>
      <input :type="type" :value="answer" :name="type" @click="$emit('inputclick', $event)">
      <span>{{answer}}</span>
    </label>
  </div>
</template>

<script>
export default {
  name: 'AppInput',
  props: ['answer', 'index', 'type']
}
</script>

<style scoped lang="scss">
  label {
    display: inline-flex;
    align-items: center;
    cursor: pointer;
  }
  input {
    margin-right: 10px;
    margin-top: 0;
    cursor: pointer;
  }
</style>