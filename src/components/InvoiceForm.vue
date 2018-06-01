<template>
  <div class="main-form">
      <label>Check No
        <input type="text" name="number" v-model="invoice.number" required/>
      </label><br>
      <label> Day
        <input type="text" name="date" v-model="invoice.dated" required/>
      </label>
      <label> Month
        <input type="text" name="date" v-model="invoice.datem" required/>
      </label>
      <label> Year
        <input type="text" name="date" v-model="invoice.datey" required/>
      </label><br>
      <label> Sum
        <input type="text" name="amount" v-model="invoice.amount" required/>
      </label><br>
      <label> Captcha
        <input type="text" name="captcha" v-model="invoice.captcha" required/>
      </label><br>
    </div>
</template>

<script>
export default {
  name: 'InvoiceForm',
  data: function () {
    return {
      invoice: {
        amount: '',
        number: '',
        captcha: '',
        dated: '',
        datem: '',
        datey: ''
      }
    }
  },
  watch: {
    invoice: {
      handler: function () {
        this.$emit('invoiceChanged', this.invoice)
      },
      deep: true
    }
  }
}
</script>
