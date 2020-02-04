<template>
  <div class="app flex-row align-items-center">
    <div class="container">
      <b-row class="justify-content-center">
        <b-col md="8">
          <b-card-group>
              <b-card-body>
                <b-form>
                  <h1 style="font-size: 62px; color:dodgerblue">Login to the system!</h1><br><br>
                  <label>
                    Email
                  </label>
                  <b-input-group class="mb-3">
                    <b-form-input type="text" class="form-control" placeholder="johndoe@mail.com" autocomplete="username email" v-model="formData.email"/>
                  </b-input-group>
                  <div class="error" id="emailErr" style="color:red; font-size: small"></div>
                  <label>
                    Password
                  </label>
                  <b-input-group class="mb-4">
                    <b-form-input type="password" class="form-control" placeholder="Password" autocomplete="current-password" v-model="formData.password"/>
                  </b-input-group>
                  <div class="error" id="passwordErr" style="color:red; font-size: small"></div>
                  <b-row>
                    <b-col align="center">
                      <b-button class="btn-default" color="white" @click="formValidation">Login</b-button>
                    </b-col>
                  </b-row>
                  <b-row>
                    <b-col class="text-center">
                      <router-link to="/forgotPassword">Forget Password?</router-link>
                    </b-col>
                  </b-row>
                </b-form>
              </b-card-body>
          </b-card-group>
        </b-col>
      </b-row>
    </div>
  </div>
</template>

<script>
  import router from "../../router/index"
  import axios from "axios"
  export default {
    name: 'login',
    data() {
      return {
        formData: {
          email: '',
          password: ''
        }
      }
    },
    methods: {
      formValidation: function () {
        //console.log(this.formData.email);
        // Retrieving the values of form elements
        const email = this.formData.email;
        const password = this.formData.password;

        // Defining error variables with a default value
        let emailErr = true;
        let passwordErr = true;

        // Validate email address
        if (email === "") {
          this.printError("emailErr", "Please enter your email address");
        } else {
          // Regular expression for basic email validation
          let regex = /^\S+@\S+\.\S+$/;
          if (regex.test(email) === false) {
            this.printError("emailErr", "Please enter a valid email address");
          } else {
            this.printError("emailErr", "");
            emailErr = false;
          }
        }
        // Validate password
        if (password === "") {
          this.printError("passwordErr", "Please enter your password");
        } else {
          let regex = /^(?=.*[A-Z])(?=.*\d).{6,12}$/;
          if (regex.test(password) === false) {
            this.printError("passwordErr", "Password must have at least a uppercase, a number between 6-12 characters");
          } else {
            this.printError("passwordErr", "");
            passwordErr = false;
          }
        }
        // Prevent the form from being submitted if there are any errors
        if ((emailErr || passwordErr) === true) {
          return false;
        } else {
          console.log("axios entering point");
          const dataObject = {
            "email": email,
            "password": password
          };
          console.log(dataObject);
          axios.post('http://localhost:7000/api/admin/login', dataObject,
            {
            headers: {
              'Content-Type': 'application/json',
            }
          })
          .then(response => {
            if(response.data.status === 200) {
              localStorage.setItem('access_token', response.data.accessToken);
              router.push("/loadDashboard");
              //this.authToken();
              //alert("success");
            } else{
              alert(response.data.message);
              router.push("/");
            }
          })

        }
      },
      printError: function (elemId, hintMsg) {
        document.getElementById(elemId).innerHTML = hintMsg;
      },

      /*authToken: function() {
        console.log("authToken");
        axios.get("http://localhost:3000/api/dashboard")
          .then((response) => {
            if(response.data.status == 200) {
              alert("Token Matched");
              router.push("/api/dashboard");
            } else {
              alert("Could not authenticate token");
              router.push("/api/login");
            }
          })
          .catch(err => {
            console.log("Error:" +err);
          })
      }*/

    }
  }
</script>
