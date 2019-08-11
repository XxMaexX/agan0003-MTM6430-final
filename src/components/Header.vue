<template>
 <div id="navigation-view">
 <ul>
     <h1>State Manager</h1>
     <!-- navigation links for each page -->
     <div id="nav">
 <li><router-link v-if="auth" :to="{ name: 'dashboard' }">Dashboard</router-link> </li>
 <li><router-link v-if="!auth" :to="{ name: 'signup' }">Sign Up</router-link></li>
 <li><router-link v-if="!auth" :to="{ name: 'signin' }">Sign In</router-link></li>
 <li><router-link :to=" { name: 'home' } ">Home</router-link> </li>
 <a v-if="auth" class="logout" @click="logout"> Log Out</a>
 </div>
     <!-- if the error is set, diaplay the div, the info of the div is the {{error}} -->
    <div class="error" @click="clearError" v-if="error">{{error}}</div>
 </ul>
 </div>
</template>

<script>
import { mapState, mapActions, mapGetters} from "vuex";
// import { METHODS } from 'http';
// set the error message as global function
export default {
  computed: {
    ...mapState(["error"]),
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

<style scoped lang='css'>

#navigation-view ul {
  padding: 45px;
}

ul h1 {
    position: absolute;
    color: white;
    margin-top: none;
    padding-left: 20px;
    left: 20px;
}

ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-color: #719bd5;
}

li {
  float: right;
}

li a {
  display: block;
  color: white;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
}

li a:hover:not(.active) {
  background-color: #2f3e65;
}

.active {
  background-color: #2f3e65;
}

</style>