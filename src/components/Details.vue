<template>
  <div class="details">
    <select name="existing-details" v-if="this.details.length > 0">
      <option v-for="(detail, index) in details"  v-bind:key="index">{{ detail.title }} {{ detail.id }}</option>
    </select>
    <DetailsForm v-if="this.addNew" @save="saveDetails" @cancel="cancelDetails"/>
    <button v-on:click="addNew = !addNew" v-if="!addNew">Add New</button>
  </div>
</template>

<script>
import DetailsForm from './DetailsForm.vue'

export default {
  name: 'Details',
  components: {
    DetailsForm
  },
  data: function () {
    return {
      details: [],
      addNew: false
    }
  },
  mounted () {
    this.getDetails()
  },
  methods: {
    getDetails () {
      let details = JSON.parse(localStorage.getItem('lp-details'))
      if (details !== null && details.length > 0) this.details = details
    },
    saveDetails (title, id, address, vat) {
      let detail = {
        'title': title,
        'id': id,
        'address': address,
        'vat': vat
      }

      this.details.push(detail)
      localStorage.setItem('lp-details', JSON.stringify(this.details))
      this.showBtn()
    },
    cancelDetails () {
      this.showBtn()
    },
    showBtn () {
      this.addNew = false
    }
  }
}
</script>
