<template>
    <div>
      <div v-bind:key="profile.id" v-for="profile in profiles">
        <ProfileItem v-bind:id="profile.id" v-bind:name="profile.name" v-bind:email="profile.email" 
        v-bind:description="profile.description"
         v-bind:profile="profile" v-on:del-profile="$emit('del-profile', profile.id)"
         v-bind:profiles="profiles"/>
      </div>
    </div>
  </template>
  
  <script>
  import ProfileItem from './ProfileItem.vue';
  export default {
    name: "Profiles",
    components: {
      ProfileItem
    },
    props: ["profiles"]
  }
  </script>
  
  <style scoped>
  </style>