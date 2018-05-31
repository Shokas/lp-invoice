<template>
  <div class="details-form">
    <label>Name / Title
      <input type="text" name="title" v-model="title" required/>
    </label><br>
    <label> ID / Code
      <input type="text" name="id" v-model="id" required/>
    </label><br>
    <label> Address
      <input type="text" name="address" v-model="address" required/>
    </label><br>
    <label> VAT code
      <input type="text" name="vat" v-model="vat" />
    </label><br>
    <button v-on:click="save()" :disabled="!disabledButton">Save</button>
    <button v-on:click="cancel()">Cancel</button>

  </div>
</template>

<script>
export default {
  name: 'DetailsForm',
  data: function () {
    return {
      title: '',
      id: '',
      address: '',
      vat: ''
    }
  },
  computed: {
    disabledButton: function () {
      return this.title.length > 0 && this.id.length > 0 && this.address.length > 0
    }
  },
  methods: {
    save () {
      this.$emit('save', this.title, this.id, this.address, this.vat)
      this.clear()
    },
    cancel () {
      this.$emit('cancel')
      this.clear()
    },
    clear () {
      this.title = ''
      this.id = ''
      this.address = ''
      this.vat = ''
    }
  }
}
</script>
