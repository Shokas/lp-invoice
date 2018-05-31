<template>
  <div id="app">
    <InvoiceForm />
    <Details />
  </div>
</template>

<script>
import InvoiceForm from './components/InvoiceForm.vue'
import Details from './components/Details.vue'

export default {
  name: 'app',
  components: {
    InvoiceForm,
    Details
  }
}
</script>
