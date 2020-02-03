<template>
  <div class="app flex-row align-items-center">
    <div class="container">
      <b-row class="justify-content-center">
        <b-col md="8">
          <b-card-group>
            <b-card-body>
              <b-form>
                <h1 style="font-size: 62px; color:dodgerblue">Forgot Password?</h1><br><br>
                <b-label>
                  Email
                </b-label>
                <b-input-group class="mb-3">
                  <b-form-input type="text" lass="form-control" placeholder="johndoe@mail.com" autocomplete="username email" />
                </b-input-group>
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
  export default {
    name: 'forgotPassword'
  }
</script>
