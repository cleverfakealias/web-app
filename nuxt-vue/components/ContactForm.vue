<template>
  <v-form @submit.prevent="submitForm">
    <v-text-field v-model="name" label="Name" required></v-text-field>
    <v-text-field v-model="email" label="Email Address" required></v-text-field>
    <v-textarea v-model="message" label="Message" required></v-textarea>
    <vue-recaptcha
      :sitekey="recaptchaSiteKey"
      @verify="onCaptchaVerified"
      @expired="onCaptchaExpired"
    ></vue-recaptcha>
    <v-btn type="submit">Submit</v-btn>
  </v-form>
</template>

<script>
import axios from 'axios'
import VueRecaptcha from 'vue-recaptcha'

export default {
  components: {
    VueRecaptcha,
  },
  data() {
    return {
      name: '',
      email: '',
      message: '',
      recaptcha: '', // Add this line
    }
  },
  computed: {
    recaptchaSiteKey() {
      return process.env.NUXT_ENV_CAPTCHA_SITE_KEY_V2
    },
  },
  methods: {
    onCaptchaVerified(response) {
      this.recaptcha = response
    },
    onCaptchaExpired() {
      this.recaptcha = ''
    },
    async submitForm() {
      if (!this.recaptcha) {
        alert('Please verify the CAPTCHA')
        return
      }
      // ...
    },
  },
}
</script>