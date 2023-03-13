<template>
  <div id="app" style="padding: 30px">
    <TagSelect 
    v-model="selectedOption"
    :options="option"
    fieldvalue="id"
    fieldlabel="label"
    />
  </div>
</template>

<script>
import TagSelect from './components/TagSelect.vue'

export default {
  name: 'App',
  components: {
    TagSelect
  },
  data() {
    return {
    option:[
      { id: 1, label: 'One' },
      { id: 2, label: 'Two' },
      { id: 3, label: 'Three'},
    ],
    };
  },
}
</script>

<style>
* {
  box-sizing: border-box;
}

body{
  font-family: Verdana, sans-serif;
}
</style>
