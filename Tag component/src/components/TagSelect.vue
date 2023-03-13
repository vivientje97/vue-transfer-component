<template>
  <div class="container">
    <details class="details" @change="onChange">
    <summary>
    <div class="containerTags">
      <div class="selectedTags" v-for="selectedOptions of selectedOption">
        <button class="btn" @click="unselect(selectedOptions)">{{ selectedOptions }} </button>
      </div>
    </div>
    </summary>
      <div class="optionList" v-for="option in options">
        <label class="optionLabel">
        <input 
          type="checkbox"
          v-model="selectedOption"
          :key="option.id"
          :value="option.id"
        >
          <span>
            {{ option.label }}
          </span>
        </label>
      </div>
    </details>
  </div>
</template>

<script>
export default {
  props: {
    options: {
      type: Array,
    },
    fieldvalue: {
      type: String,
    },
    fieldlabel: {
      type: String,
    },
  },
  data() {
    return {
      selectedOption: [],
      selectedOptions: [],
    };
  },
  methods: {
    unselect: function(selectedOptions) {
      this.selectedOption = this.selectedOption.filter(value => value !== selectedOptions);
    },
  },
};
</script>
<style>
input,
input:checked,
input:checked + span{
  display: none;
}

.selectedTags{
  float: left;
}

.containerTags {
  border: 1px #ddd solid;
  height: 24px;
}

summary {
  display: list-item;
  list-style: disclosure-closed;
}
details[open] > summary {
  list-style: disclosure-open;
}

.optionList:hover{
  background-color: lightgrey;
}

.container{
  border: 1px #ddd solid;
  width: 300px;
}

.optionLabel{
  cursor: pointer;
}

.btn{
  display: inline-block;
  border-radius: 4px;
  background-color: #EE7200;
  border: none;
  color: #FFFFFF;
  text-align: center;
  width: 40px;
  cursor: pointer;
  margin: 0 2px;
}

.btn:hover::after {
  content: ' x';
}
</style>