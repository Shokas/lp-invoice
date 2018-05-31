<template>
  <div class="main-form">
    <div v-html="body">

    </div>
  </div>
</template>

<script>
var cheerio = require('cheerio')

export default {
  name: 'InvoiceForm',
  data: function () {
    return {
      body: ''
    }
  },
  mounted () {
    this.getForm()
  },
  methods: {
    getForm () {
      this.axios.get('/sf').then((response) => {
        this.body = response.data

        var $ = cheerio.load(response.data)
        var $form = $('.invoices-form')

        this.body = $form.html()
      })
    }
  }
}
</script>
