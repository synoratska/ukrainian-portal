<template>
  <div class="reset-password">
   <Modal v-if="modalActive" :modalMessage="modalMessage"  v-on:close-modal="closeModal"/>
   <Loading v-if="loading" />
    <div class="form-wrap">
      <form class="reset">
        <p class="login-register">
        Don't have an account yet?
        <router-link class="router-link" :to="{ name: 'Login' }">
          Login
        </router-link>
      </p>
        <h2>Reset Password</h2>
        <p>Forgot your password? Enter your email to reset it.</p>
        <div class="inputs">
          <div class="input">
            <input type="text" placeholder="Email" v-model="email" />
            <email class="icon" />
          </div>
        </div>
        <button @click.prevent="resetPassword">Reset</button>
        <div class="angle"></div>
      </form>
      <div class="background"></div>
    </div>
  </div>
</template>

<script>

import Modal from '@/components/Modal'
import email from '@/assets/Icons/envelope-regular.svg'
import Loading from '@/components/Loading'
import firebase from 'firebase/app'
import 'firebase/auth'
export default {
  name: 'ForgotPassword',
  components: {
    email,
    Modal,
    Loading
  },
  data() {
   return {
    email: '',
    modalActive: false,
    modalMessage: '',
    loading: null,
   }
  },
  methods: {
   closeModal() {
    this.modalActive = !this.modalActive
    this.email = ''
   },
   resetPassword(){
    this.loading = true
    firebase.auth().sendPasswordResetEmail(this.email).then(() => {
      this.modalMessage = 'If your account exists, you will receive an email'
      this.loading = false
      this.modalActive = true
    }).catch(err => {
      this.modalMessage = err.message
      this.loading = false
      this.modalActive = true
    })
   }
  }
}
</script>

<style lang="scss" scoped>
.reset-password {
  position: relative;

  .form-wrap {
    .reset {
      h2 {
        margin-bottom: 8px;
      }

      p {
        text-align: center;
        margin-bottom: 32px;
      }
    }
  }
}

  .background {
    display: none;
    flex: 2;
    background-size: cover;
    background-image: url('@/assets/bg-reset.jpeg');
    width: 100%;
    height: 100%;

    @media (min-width: 900px) {
      display: initial;
    }
  }
</style>
