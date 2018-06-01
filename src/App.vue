<template>
  <div id="app">
    <Invoice v-bind="details" />
    <Details @detailsChanged="setDetails"/>
  </div>
</template>

<script>
import Invoice from './components/Invoice.vue'
import Details from './components/Details.vue'

export default {
  name: 'app',
  components: {
    Invoice,
    Details
  },
  data () {
    return {
      details: {
        address: '',
        title: '',
        id: '',
        vat: ''
      }
    }
  },
  methods: {
    setDetails (data) {
      this.details.address = data.address
      this.details.title = data.title
      this.details.id = data.id
      this.details.vat = data.vat
    }
  }
}
</script>
