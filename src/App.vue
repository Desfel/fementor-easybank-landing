<template>
  <div id="app" :class="{'is-open' : isOpen}">
    <nav-bar @triggerBurger="triggerBurger"></nav-bar>
    <div class="main-wrapper">
      <router-view />
    </div>

    <new-content-available-toastr
      v-if="newContentAvailable"
      class="new-content-available-toastr"
      :refreshing-app="refreshingApp"
      @refresh="serviceWorkerSkipWaiting"
    ></new-content-available-toastr>
    <apple-add-to-home-screen-modal
      v-if="showAddToHomeScreenModalForApple"
      class="apple-add-to-home-screen-modal"
      @close="closeAddToHomeScreenModalForApple(false)"
    >
    </apple-add-to-home-screen-modal>
  </div>
</template>
<script>
import NavBar from '@/components/NavBar'
import NewContentAvailableToastr from '@/components/NewContentAvailableToastr'
import AppleAddToHomeScreenModal from '@/components/AppleAddToHomeScreenModal'
import { mapState, mapGetters } from 'vuex'

export default {
  data() {
    return {
      isOpen: false
    }
  },
  components: { NavBar, NewContentAvailableToastr, AppleAddToHomeScreenModal },
  computed: {
    ...mapGetters('app', ['newContentAvailable']),
    ...mapState('app', ['showAddToHomeScreenModalForApple', 'refreshingApp'])
  },
  methods: {
    triggerBurger(value) {
      this.isOpen = value
    }
  }
}
</script>

<style lang="scss">
@import '@/theme/variables.scss';

body {
  margin: 0;

  * {
    box-sizing: border-box;
  }

  img {
    vertical-align: middle;
  }

  p,
  h1,
  h2,
  h3,
  a {
    font-family: $textFont;
    margin: 0;
  }

  a {
    text-decoration: none;
  }

  .site-btn {
    width: fit-content;
    padding: 8px 33px;
    font-weight: bold;
    font-size: 14px;
    line-height: 28px;
    color: $white;
    background: $gradient;
    border-radius: 22px;
    transition: opacity .3s ease-in-out;

    &:hover {
      opacity: .4;
    }
  }

  #app {
    position: relative;
    font-family: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, Oxygen,
      Ubuntu, Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    font-size: 16px;
    color: #2c3e50;
    background: $white;

    .new-content-available-toastr {
      position: absolute;
      bottom: 10px;
      right: 10px;
    }

    .main-wrapper {
      .page-wrapper {
        margin: auto;
      }
    }

    &.is-open {
      &:before {
        opacity: 1;
        pointer-events: auto;
      }
    }

    &:before {
      content: '';
      position: fixed;
      top: 0;
      left: 0;
      background: linear-gradient(180deg, #2D314D 0%, rgba(45, 49, 77, 0.0001) 100%);
      height: 100vh;
      width: 100%;
      z-index: 10;
      opacity: 0;
      pointer-events: none;
      transition: opacity .3s ease-in-out;
    }
  }
}
</style>
