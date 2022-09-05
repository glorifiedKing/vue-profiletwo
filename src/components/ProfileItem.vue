<template>
  <div class="container">
  <div class="profile-item" v-bind:class="{'is-complete':profile.name}">
    <p>
      <input type="checkbox" v-on:change="markComplete" v-bind:checked="profile.completed">
      {{profile.name}}
      <button @click="$emit('del-profile', profile.id)" class="del">x</button>
      </p>
  </div>
  </div>
</template>
 
<script>
export default {
  name: "ProfileItem",
  props: ["profile"],
  methods: {
    markComplete() {
      this.profile.completed = !this.profile.completed;
    }
  }
}
</script>
 
<style scoped>
  .profile-item {
    background: #f4f4f4;
    padding: 10px;
    margin:20px;
    border-bottom: 1px #ccc dotted;
  }
 
  .is-complete {
    text-decoration: line-through;
  }
 
  .del {
    background: #ff0000;
    color: #fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
  }
</style>
