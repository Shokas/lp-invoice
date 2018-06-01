<template>
  <div class="invoice">
    <InvoiceForm @invoiceChanged="changeData"/>
    <img :src="'https://post.lt' + url" />
    <button v-on:click="getBasketID">Get Invoice</button>
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
      token: '',
      bid: '',
      url: ''
    }
  },
  mounted () {
    this.getInitialForm()
  },
  methods: {
    getInitialForm () {
      this.axios.get('/sf').then((response) => {
        var $ = cheerio.load(response.data)

        this.fid = $('#fid').val()
        this.fid2 = $('#fid2').val()
      })
      this.refreshCaptcha()
    },
    refreshCaptcha () {
      this.axios.get('/refresh').then((response) => {
        this.sid = response.data.data.sid
        this.token = response.data.data.token
        this.url = response.data.data.url
      })
    },
    changeData (data) {
      this.amount = data.amount
      this.number = data.number
      this.captcha = data.captcha
      this.dated = data.dated
      this.datem = data.datem
      this.datey = data.datey
    },
    getBasketID () {
      let data = {
        'amount': this.amount,
        'captcha': this.captcha,
        'dated': this.dated,
        'datem': this.datem,
        'datey': this.datey,
        'fid': this.fid,
        'number': this.number,
        'sid': this.sid,
        'token': this.token,
        'step': '1'
      }

      this.axios.post('/invoice', data).then((response) => {
        console.log(response)
        // this.bid = response.GetBasketResult.BasketInfo.ID
        this.sid = response.data.error.captcha.sid
        this.token = response.data.error.captcha.token
        this.url = response.data.error.captcha.url
      })
    }
  }
}
</script>
