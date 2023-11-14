<template>
     <div class="section">
      <p class="header">Add new profile:</p>
      <div class="flex-row">
        <label class="label">Name:</label>
        <input class="input" v-model="name">
      </div>
      <div class="flex-row">
        <label class="label" for="filter">Email:</label>
        <input class="input" v-model="email">
      </div>
      <div class="flex-row">
        <label class="label">Specialisation:</label>
        <input class="input" v-model="specialization">
      </div>
      <button v-on:click="addProfile">Add</button>
    </div>
</template>

<script>
    export default {
  name: "App",

 
  emits: ['new-profile'],

  data() {
    return {
        name: '',
        email: '',
        specialization: ''
    }
  },
  methods: {
    addProfile(){
        this.$emit('new-profile', {name: this.name, email: this.email, specialization: this.specialization})
        this.name = ''
        this.email = ''
        this.specialization = ''
    }
  }
}
</script>