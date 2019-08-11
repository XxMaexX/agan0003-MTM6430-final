<template>
<!-- start of form -->
  <div id="userForm">
    <h1>Sign In</h1>
    <div id="basicForm">
    <form @submit.prevent="onSubmit">
      <!-- Input email in the form -->
      <div>
        <label for="email">Email</label>
        <input type="email" v-model="email" id="email" requried />
      </div>
      <!-- Input password in the form -->
      <div>
        <label for="pass">Password</label>
        <input type="password" v-model="pass" id="pass" requried />
      </div>
      <!-- once form is completed, user's must click the submit button and will bring them to the dashboard page -->
      <button type="submit">Submit</button>
    </form>
    </div>
  </div>
</template>

<script>
import { mapActions } from "vuex";
export default {
  data() {
    return {
      email: "",
      pass: ""
    };
  },
  methods: {
    ...mapActions(["signIn"]),
    onSubmit() {
      const formData = {
        email: this.email,
        password: this.pass
      };

      this.signIn(formData);
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

#basicForm button {
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

#basicForm button:hover {
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
