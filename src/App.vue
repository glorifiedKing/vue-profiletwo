<template>
  <div id="app">
    <p>Profiles List</p>
    <div class="section">
      <div class="flex-row">
        <label class="label" for="filter">Find profile:</label>
        <input class="input" id="filter" v-model="filter">
      </div>
      <div class="buttons">
        <button @click="sortAsc">▲</button>
        <button @click="sortDesc">▼</button>
      </div>

      <ProfileCard
        v-for="(profile, index) in filteredProfiles"
        :key="index"
        :profile="profile"
        class="profile"
        @comment="commentChanged(profile, $event)"
      />

      <div class="icons-note">
        Icons made by
        <a href="https://www.flaticon.com/authors/freepik" title="Freepik">Freepik</a> from
        <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a>
      </div>
    </div>

    <div class="section">
      <p class="header">Add new profile:</p>
      <div class="flex-row">
        <label class="label">Name:</label>
        <input class="input" type="text" v-model="newProfile.name">
      </div>
      <div class="flex-row">
        <label class="label">Email:</label>
        <input class="input" type="email" v-model="newProfile.email">
      </div>
      <div class="flex-row">
        <label class="label">Specialisation:</label>
        <input class="input" type="text" v-model="newProfile.description">
      </div>
      <button @click="addProfile">Add</button>
    </div>
  </div>
</template>

<script>
import ProfileCard from "./components/ProfileCard";

export default {
  name: "App",

  components: {
    ProfileCard
  },

  data() {
      return {
          profiles: [
              {
                  id: 1,
                  name: "Wojciech",
                  email: "wojciech@poz.pl",
                  description: "Anaesthesiologist",
                  likes: 34
              },
              {
                  id: 2,
                  name: "Maria",
                  email: "maria@poz.pl",
                  description: "Radiologist",
                  likes: 28
              },
              {
                  id: 3,
                  name: "Anna",
                  email: "anna@poz.pl",
                  description: "Surgeon",
                  likes: 53
              }
          ],
          filter: '',
          newProfile: {
              id: '',
              name: '',
              email: '',
              description: '',
              likes: 0,
              comment: ''
          }
      };
  },

  methods: {
      sortAsc() {
          this.profiles.sort(function (a, b) {
              return a.likes - b.likes;
          });
      },

      sortDesc() {
          this.profiles.sort(function (a, b) {
              return b.likes - a.likes;
          });
      },
      commentChanged(prof, com) {
          const itemIndex = this.profiles.findIndex((t) => t.id === prof.id);
          this.profiles[itemIndex].comment = com;
      },
      addProfile() {
          this.newProfile.id = this.profiles.length+2;
          this.profiles.push(this.newProfile);
      }
  },
    computed: {
      filteredProfiles() {
          if (this.filter === '') {
              return this.profiles;
          }

          return this.profiles.filter((t) => t.name.toLowerCase().includes(this.filter.toLowerCase()));
      }
    }
};
</script>

<style>
#app {
  font-family: "Roboto", helvetica, arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  padding: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  position: relative;

  background: linear-gradient(
    135deg,
    rgba(65, 184, 131, 0.9),
    rgba(52, 73, 94, 0.9)
  );

  font-size: 1.5em;
}

button {
  display: block;
  padding: 1em;
  width: 100%;
  background-color: #41B883;
  border: 1px solid;
  color: #fff;
  cursor: pointer;
  font-size: 0.75em;
  font-weight: 600;
  text-shadow: 0 1px 0 rgba(black, 0.2);
}

.content {
  display: flex;
}

.section {
  width: 100%;
  min-width: 300px;
  padding: 2em;
  margin-top: 30px;
  position: relative;
  background: rgba(0, 0, 0, 0.15);
}

@media screen and (min-width: 600px) {
  .section {
    width: 50vw;
    max-width: 15em;
  }
}

.header {
  color: #fff;
}

.section::before {
  content: "";
  position: absolute;
  top: -2px;
  left: 0;
  height: 2px;
  width: 100%;
  background: #35c3c1;
}

.flex-row {
  display: flex;
  margin-bottom: 1em;
}

.label {
  width: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 12px;

  background: #f5f6f8;
}

.input {
  flex: 1;
  padding: 1em;
  border: 0;
  color: #8f8f8f;
  font-size: 1rem;
}

.buttons {
  display: flex;
  box-shadow: 0 10px 10px rgba(0, 0, 0, 0.25), 0 5px 5px rgba(0, 0, 0, 0.22);
  margin-top: 30px;
}

.profile {
  margin-top: 20px;
}

.icons-note {
  margin-top: 30px;
  font-size: 10px;
}
</style>
