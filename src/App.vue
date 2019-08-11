<template>
  <div id="app">
    <div id="topNav">
      <ul>
        <h1>State Manager</h1>
          <div id="nav">
            <li><router-link :to="{ name: 'home' }">Home</router-link></li>
            <li><router-link v-if="!auth" :to="{ name: 'signup' }">Sign Up</router-link></li>
            <li><router-link v-if="!auth" :to="{ name: 'signin' }">Sign In</router-link></li>
            <li><router-link v-if="auth" :to="{ name: 'dashboard' }">Dashboard</router-link></li>
            <li><a v-if="auth" class="logout" @click="logout"> Log Out</a></li>
          </div>
      </ul>
    </div>
    <!-- if the error is set, diaplay the div, the info of the div is the {{error}} -->
    <div class="error" @click="clearError" v-if="error">{{error}}</div>
      <router-view />
    <div id="bottomBanner">
      <p> © Copyrights - MySite 2019</p>
    </div>
  </div>
</template>

<script>
import { mapState, mapActions, mapGetters} from "vuex";
// import { METHODS } from 'http';
// set the error message as global function
export default {
  computed: {
    ...mapState(["error"]),
// sign in dashboard，sign in sign up
    ...mapGetters({
      auth: "isauthenticated"
    })
  },

  methods: {
    ...mapActions(["clearError", "logout", "autoLogin"])
  },
  created() {
    this.autoLogin();
  }
};
</script>

<style>
#app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    max-width: 1024px;
    margin: 0 auto;
}

#topNav {
  background-color: #719bd5;
  width: 100vw;
  position: relative;
  margin-left: -50vw;
  height: 100px;
  left: 50%;
}

#topNav ul {
  padding: 45px;
}

#topNav ul h1 {
    position: absolute;
    color: white;
    margin-top: none;
    padding-left: 20px;
    left: 20px;
}

#topNav ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-color: #719bd5;
}

#nav li {
  float: right;
}

#nav li a {
  display: block;
  color: white;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
}

#nav li a:hover:not(.active) {
  background-color: #2f3e65;
}

.active {
  background-color: #2f3e65;
}

.error {
    background-color: rosybrown;
    padding: 20px;
}

#bottomBanner p {
  float: right;
  padding: 15px;
}

#bottomBanner {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  background-color: #719bd5;
  color: white;
  text-align: center;
}
</style>
