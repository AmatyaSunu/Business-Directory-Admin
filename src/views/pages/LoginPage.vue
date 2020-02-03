<template>
  <div class="app flex-row align-items-center">
    <div class="container">
      <b-row class="justify-content-center">
        <b-col md="8">
          <b-card-group>
              <b-card-body>
                <b-form>
                  <h1 style="font-size: 62px; color:dodgerblue">Login to the system!</h1><br><br>
                  <b-label>
                    Email
                  </b-label>
                  <b-input-group class="mb-3">
                    <b-form-input type="text" lass="form-control" placeholder="johndoe@mail.com" autocomplete="username email" />
                  </b-input-group>
                  <b-label>
                    Password
                  </b-label>
                  <b-input-group class="mb-4">
                    <b-form-input type="password" class="form-control" placeholder="Password" autocomplete="current-password" />
                  </b-input-group>
                  <b-row>
                    <b-col align="center">
                      <b-button class="btn-default" color="white" @click="$router.push('/dashboard')">Login</b-button>
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

  export default {
    name: 'login'
  }
</script>
