<template>
  <div id="app">
	  <spinner :initial-value="initialValue" :step="step" :allow-negatives="allowNegatives" :input-editable="inputEditable" :show-buttons="showButtons" :direction="direction" :min="min" :max="max" :readonly="readonly" :disabled="disabled" :required="required"></spinner>
  </div>
</template>

<script>
import spinner from './components/spinner/spinner.vue'

export default {
  name: 'app',
  components: {
    spinner
  },
  data() {
	  return {
		  initialValue: 0,
		  step: 1,
		  allowNegatives: false,
		  inputEditable: true,
		  showButtons: true,
		  direction: "vertical",
		  min: 0,
		  max: false,
		  readonly: false,
		  disabled: false,
		  required: true,
	  }
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
