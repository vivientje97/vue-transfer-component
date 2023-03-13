<template>
  <div id="app">
    <transfer
    leftTitle="Source"
    rightTitle="Target"
    :filters="leftData"
    :filtersRight="rightData"
    :showItemCount="true"
    :showSelectCount="true"
    :showSelectAll="true"
    />
  </div>
</template>

<script>
import transfer from './components/transfer.vue'

export default {
  name: 'App',
  components: {
    transfer
  },
  data() {
    return {
      leftData: [
        'Campina',
        'Douwe Egberts',
        'Coca-Cola',
        'Heineken',
        'Unox',
        'Dr Oetker',
        'Amstel',
        'Knorr',
        'Lipton',
        'Spa',
        'Heinz',
        'Calvé',
      ],
      rightData: [],
    }
  }
}
</script>

<style>

</style>
