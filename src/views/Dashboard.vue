<template>
<!-- start of form -->
    <div id="userForm">
        <h1>Dashboard</h1>
        <!-- Display what user answered in the form -->
        <p>Welcome to your dashboard {{ user.name }}! </p>
        <p> Your age is: {{ user.age }} </p>
        <p> Your city is: {{ user.city }} </p>
        <p> Your job is: {{ user.job }} </p>
        <p> Your login email is: {{ user.email }} </p>
        <div id="basicForm">
        <form @submit.prevent="submitForm" >
            <!-- Change name in the form -->
            <label for="name">Edit your name:</label>
            <input type="text" id="name" v-model="user.name" >
            <br /> 
            <!-- Change age in the form -->
            <label for="age">Edit your age:</label>
            <input type="text" id="age" v-model="user.age" >
            <br /> 
            <!-- Change city in the form -->
            <label for="city">Edit your city:</label>
            <input type="text" id="city" v-model="user.city" >
            <br /> 
            <!-- Change job in the form -->
            <label for="job">Edit your job:</label>
            <input type="text" id="job" v-model="user.job" >
            <br /> 
            <!-- Once user is completed filling the text field, they must click the submit button to upadate any changes in the form -->
            <input type="submit" value="Submit" >
        </form>
        </div>
    </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
export default {
    computed: {
        ...mapGetters({
            userData: "getUser"
        }),
        user() {
            return !this.userData ? false : this.userData;
        }
    },
    created(){
        this.getUserData();
    },
    methods: {
        ...mapActions(["fetchUser", "updateUser"]),
        getUserData() {
            let userEmail = localStorage.getItem("userEmail");
            this.fetchUser(userEmail);
        },
        submitForm() {
            this.updateUser();
        }
    }
};
</script>

<style>
#userForm {
  max-width: 500px;
  width:100%;
	margin: 50px auto;
  margin-bottom: 200px;
	position: relative;
  border-radius: 20px;
  background-color: #f2f2f2;
  padding: 40px;
  padding-bottom: 50px;
}

#userForm h1 {
  display: flex;
}

#basicForm input[type=text], input[type=email], input[type=password], select {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

#basicForm input[type=submit] {
  float: right;
  width: 50%;
  background-color: #719bd5;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

#basicForm input[type=submit]:hover {
  background-color: #003f5a;
}

#basicForm {
  padding: 20px;
}

#basicForm .el-button--primary {
    float: right;
    margin-bottom: 10px !important;
  }
</style>
