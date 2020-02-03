<template>
  <div class="app flex-row align-items-center">
    <div class="container">
      <b-row class="justify-content-center">
        <b-col md="8">
          <b-card-group>
            <b-card-body>
              <b-form>
                <h1 style="font-size: 62px; color:dodgerblue">Forgot Password?</h1><br><br>
                <label>
                  Email
                </label>
                <b-input-group class="mb-3">
                  <b-form-input type="text" lass="form-control" placeholder="johndoe@mail.com" autocomplete="username email" v-model="formData.email"/>
                </b-input-group>
                <div class="error" id="emailErr" style="color:red; font-size: small"></div>
                <b-row>
                  <b-col align="center">
                    <b-button class="btn-default" color="white" style="text-decoration-color: dodgerblue">Send Reset Link</b-button>
                  </b-col>
                </b-row>
                <b-row>
                  <b-col class="text-center">
                    <b-button variant="link">Forgot password?</b-button>
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
  import router from '../../router/index'
  import axios from 'axios'
  export default {
    name: 'forgotPassword',
    data() {
      return {
        formData: {
          email: ''
        }
      }
    },
    methods: {
      formValidation: function () {
        // Retrieving the values of form elements
        const email = this.formData.email;

        // Defining error variables with a default value
        let emailErr = true;

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

        // Prevent the form from being submitted if there are any errors
        if ((emailErr ) === true) {
          return false;
        } else {
          console.log("axios entering point");
          const dataObject ={
            "email": email
          };
          axios.post('http://localhost:7000/api/admin/forgotPassword', dataObject,
            {
              headers: {
                'Content-Type' : 'application/json'
              }
            })
          .then(response => {
            if (response.data.status === 205) {
                alert(response.data.message);
                //alert("Reset Link has been sent to your email");
                router.push("/");
            }else {
                alert(response.data.message);
            }
          })
        }
      },
      printError: function (elemId, hintMsg) {
        document.getElementById(elemId).innerHTML = hintMsg;
      }
      }

  }


</script>
