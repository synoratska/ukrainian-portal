<template>
  <div class="app-wrapper">
    <div class="app" v-if="this.$store.state.noteLoaded">
      <Navigation v-if="!navigationDisabled" />
      <router-view />
      <Footer v-if="!navigationDisabled" />
    </div>
  </div>
</template>

<script>
import Navigation from '@/components/Navigation'
import Footer from '@/components/Footer'
import firebase from 'firebase/app'
import 'firebase/auth'
export default {
  name: 'app',
  components: {
    Navigation,
    Footer,
  },
  data() {
    return {
      navigationDisabled: null,
    }
  },
  created() {
    firebase.auth().onAuthStateChanged((user) => {
      this.$store.commit('updateUser', user)
      if (user) {
        this.$store.dispatch('getCurrentUser', user)
      }
    })
    this.checkRoute()
    this.$store.dispatch('getNote')
  },
  mounted() {},
  methods: {
    checkRoute() {
      if (
        this.$route.name === 'Login' ||
        this.$route.name === 'Signup' ||
        this.$route.name === 'ForgotPassword'
      ) {
        this.navigationDisabled = true
        return
      }
      this.navigationDisabled = false
    },
  },
  watch: {
    $route() {
      this.checkRoute()
    },
  },
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@300;400;500;600;700&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Quicksand', sans-serif;
 
}

.app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.container {
  max-width: 1440px;
  margin: 0 auto;
}

.link {
  cursor: pointer;
  text-decoration: none;
  text-transform: uppercase;
  color: #000;
}

.link-light {
  color: #fff;
}

.arrow {
  margin-left: 8px;
  width: 12px;
  path {
    fill: #000;
  }
}

.arrow-light {
  path {
    fill: #f7faa5;
  }
}

span {
  color: #000 !important;
}

button,
.router-button {
  transition: 500ms ease all;
  cursor: pointer;
  margin-top: 24px;
  padding: 12px 24px;
  background-color: #303030;
  color: #f7faa5;
  border-radius: 10px 0;
  border: none;
  text-transform: uppercase;

  &:focus {
    outline: none;
  }

  &:hover {
    background-color: #303030b3;
  }
}

.button-ghost {
  color: #000;
  padding: 0;
  border-radius: 0;
  margin-top: 50px;
  font-size: 15px;
  font-weight: 500;
  background-color: transparent;

  @media (min-width: 700px) {
    margin-top: 0;
    margin-left: auto;
  }

  i {
    margin-left: 8px;
  }
}

.button-light {
  background-color: transparent;
  border: 2px solid #fff;
  color: #fff;
}

.button-inactive {
  pointer-events: none !important;
  cursor: none !important;
  background-color: #80808080 !important;
}

.error {
  text-align: center;
  font-size: 12px;
  color: #ce1313;
}

.note-card-wrap {
  position: relative;
  padding: 80px 16px;
  background: linear-gradient(-45deg, #dcd628, #bdbd07, #1a529c, #0b0e6b  );
  background-size: cover;
  background-position: center top;
  
  @media (min-width: 500px) {
    padding: 100px 16px;
  }

  .note-cards {
    display: grid;
    gap: 32px;
    grid-template-columns: 1fr;

    @media (min-width: 500px) {
      grid-template-columns: repeat(2, 1fr);
    }

    @media (min-width: 900px) {
      grid-template-columns: repeat(3, 1fr);
    }

    @media (min-width: 1200px) {
      grid-template-columns: repeat(4, 1fr);
    }
  }
}

</style>
