<template>
  <div class="invoice">
    <InvoiceForm @invoiceChanged="changeData"/>
    <img :src="'https://post.lt/' + url" />
  </div>
</template>

<script>
import InvoiceForm from './InvoiceForm.vue'
var cheerio = require('cheerio')

export default {
  name: 'Invoice',
  components: {
    InvoiceForm
  },
  props: ['title', 'id', 'address', 'vat'],
  data: function () {
    return {
      amount: '',
      number: '',
      captcha: '',
      dated: '',
      datem: '',
      datey: '',
      client_type: 'PhysicalPerson',
      fid: '',
      fid2: '',
      sid: '',
      step: '1',
      token: '',
      bid: '',
      url: '',
      search: 'https://www.post.lt/lt/invoices/search'
    }
  },
  mounted () {
    this.getInitialForm()
  },
  methods: {
    getInitialForm () {
      this.axios.get('/sf').then((response) => {
        this.body = response.data

        var $ = cheerio.load(response.data)
        this.fid = $('#fid').val()
        this.fid2 = $('#fid2').val()
        this.sid = $('#captcha_sid').val()
        this.token = $('#captcha_sid').val()
        this.url = $('#captcha_url').attr('src')
      })
    },
    changeData (data) {
      this.amount = data.amount
      this.number = data.number
      this.captcha = data.captcha
      this.dated = data.dated
      this.datem = data.datem
      this.datey = data.datey
    }
  }
}
</script>
