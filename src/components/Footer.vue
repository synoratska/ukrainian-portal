<template>
  <footer>
    <div class="container">
      <div class="left">
        <div class="col-1">
          <router-link class="header" :to="{ name: 'Home' }"
            >Ukrainian <span>Portal</span></router-link
          >
        </div>
        <div class="col-2">
          <ul>
            <router-link class="link" :to="{ name: 'Home' }">Home</router-link>
            <router-link class="link" :to="{ name: 'Places' }"
              >Places</router-link
            >
            <router-link class="link" :to="{ name: 'CreateNote' }"
              >Create A Note</router-link
            >
            <router-link v-if="admin" class="link" :to="{ name: 'Home' }"
              >Gallery</router-link
            >
            <router-link v-if="!user" class="link" :to="{ name: 'Login' }"
              >Login/Register</router-link
            >
          </ul>
        </div>
      </div>
      <div class="right">
        <ul>
          <li>
            <a href="#"><youTube class="svg-icon" /></a>
          </li>
          <li>
            <a href="#"><twitter class="svg-icon" /></a>
          </li>
          <li>
            <a href="#"><instagram class="svg-icon" /></a>
          </li>
          <li>
            <a href="#"><linkedIn class="svg-icon" /></a>
          </li>
        </ul>
        <p>Copyright 2023 All Rights Reserved</p>
      </div>
    </div>
  </footer>
</template>

<script>
import youTube from '../assets/Icons/youtube-brands.svg'
import twitter from '../assets/Icons/twitter-brands.svg'
import instagram from '../assets/Icons/instagram-brands.svg'
import linkedIn from '../assets/Icons/linkedin-brands.svg'

export default {
  name: 'FooterVue',
  components: {
    youTube,
    twitter,
    instagram,
    linkedIn,
  },
  computed: {
    user() {
      return this.$store.state.user
    },
    admin() {
      return this.$store.state.profileAdmin
    },
  },
}
</script>

<style lang="scss" scoped>
footer {
  margin-top: auto;
  padding: 50px 25px 30px;
  background-color: #020202;

  @media (max-width: 800px) {
    padding-top: 40px;
    padding-bottom: 20px;
  }
  .container {
    display: flex;
    flex-direction: column;
    gap: 32px;
    @media (min-width: 800px) {
      flex-direction: row;
      gap: 0;
    }

    > div {
      display: flex;
      flex: 1;
    }

    .left {
      gap: 32px;
      color: #fff;
      display: flex;
      flex-direction: column;
      align-items: center;
      @media (min-width: 800px) {
        flex-direction: row;
        align-items: initial;
        gap: 0;
      }
      .header {
        text-align: center;
        font-size: 24px;
        color: #200a66;
        text-decoration: none;
        font-weight: 600;
        @media (min-width: 800px) {
          text-align: initial;
        }
      }
      ul {
        gap: 16px;
        list-style: none;
        display: flex;
      }

      .col-1,
      .col-2 {
        gap: 32px;
        display: flex;
        flex: 1;
        @media (min-width: 800px) {
          gap: 0;
        }
      }

      .col-1 {
        flex-direction: column;

        h2 {
          text-align: center;
          @media (min-width: 800px) {
            text-align: initial;
          }
        }
      }

      .col-2 {
        ul {
          height: 100%;
          justify-content: center;
          flex-direction: row;
          flex-wrap: wrap;
          @media (min-width: 800px) {
            flex-direction: column;
          }

          .link {
            font-size: 16px;
            font-weight: 500;
            color: #fff;
            text-decoration: none;
          }
        }
      }
    }

    .right {
      gap: 32px;
      color: #fff;
      align-items: center;
      flex-direction: column;
    
      @media (min-width: 800px) {
        align-items: flex-end;
        gap: 0;
      }
      p {
        margin-top: auto;
        font-size: 12px;
      }
      ul {
       /* margin-bottom: 30px; */
         display: flex;
        li {
          display: flex;
          align-items: center;
          justify-content: space-between;
          margin: 5px;
          .svg-icon {
            width: 24px;
            height: auto;
            color: #fff;
          }
          @media (max-width: 800px) {
            display: flex;
          }
        }
      }
    }
  }

  .header span {
    color: #ccd313 !important;
  }
}
</style>
