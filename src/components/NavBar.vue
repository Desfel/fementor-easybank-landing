<template>
  <header class="navbar">
    <router-link class="logo" to="/home">
      <img src="@/assets/img/logo.svg" alt="Easybank" />
    </router-link>
    <div class="links">
      <nav class="nav-links">
        <div class="nav-item">
          <router-link to="/home">Home</router-link>
          <router-link to="#">About</router-link>
          <router-link to="#">Contact</router-link>
          <router-link to="#">Blog</router-link>
          <router-link to="#">Career</router-link>
        </div>
      </nav>
    </div>

    <a href="#" class="site-btn">Request invite</a>
    <span class="burger-trigger" @click="openBurger">
      <img v-if="!isOpen" src="@/assets/img/icon-hamburger.svg" />
      <img v-if="isOpen" src="@/assets/img/icon-close.svg" />
    </span>

    <div class="mobile-nav" :class="{'is-open': isOpen}">
      <nav>
        <router-link to="/home">Home</router-link>
        <router-link to="#">About</router-link>
        <router-link to="#">Contact</router-link>
        <router-link to="#">Blog</router-link>
        <router-link to="#">Career</router-link>
      </nav>
    </div>
  </header>
</template>

<script>
import { mapState } from 'vuex'

export default {
  data() {
    return {
      isOpen: false
    }
  },
  methods: {
    openBurger(e) {
      e.preventDefault()
      this.isOpen = !this.isOpen
      this.$emit('triggerBurger', this.isOpen)
    }
  },
  computed: {
    ...mapState('app', [ 'appTitle', 'appShortTitle'])
  },
}
</script>

<style lang="scss" scoped>
@import '@/theme/variables.scss';

.navbar {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: $white;
  padding: 18px 10%;
  z-index: 20;

  @media (max-width: 1024px) {
    padding: 18px 40px;
  }

  @media (max-width: 800px) {
    position: fixed;
  }

  .site-btn {
    @media(max-width: 800px) {
      display: none;
    }
  }

  .logo,
  .burger-trigger {
    position: relative;
    z-index: 20;
  }

  .burger-trigger {
    cursor: pointer;

    @media (min-width: 801px) {
      display: none;
    }
  }

  .links {
    @media(max-width: 800px) {
      display: none;
    }

    .nav-links {
      .nav-item {
        a {
          position: relative;
          font-weight: normal;
          font-size: 14px;
          line-height: 16px;
          letter-spacing: -0.107692px;
          color: $neutralColor1;
          transition: color .3s ease-in-out;

          &:not(:last-child) {
            margin-right: 30px;
          }

          &:hover {
            color: $primaryColor2;

            &:before,
            &:after {
              width: 50%;
            }
          }

          &:before,
          &:after {
            content: '';
            position: absolute;
            bottom: calc(-100% - 15px);
            width: 0;
            height: 4px;
            transition: all .3s ease-in-out;
          }

          &:before {
            left: 0;
            background: linear-gradient(135deg, #33d35e 0%, #2ab6d9 99.58%);
          }

          &:after {
            right: 0;
            background: linear-gradient(135deg, #2ab6d9 0%, #33d35e 99.58%);
          }
        }
      }
    }
  }

  .mobile-nav {
    position: fixed;
    top: -450px;
    left: 24px;
    display: flex;
    width: calc(100% - 48px);
    padding: 32px 24px;
    background: $white;
    border-radius: 4px;
    text-align: center;
    z-index: 11;
    transition: all .5s ease-in-out;
    pointer-events: none;
    opacity: 0;

    &.is-open {
      top: 80px;
      opacity: 1;
      pointer-events: auto;
    }

    nav {
      width: 100%;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;

      a {
        font-weight: normal;
        font-size: 18px;
        line-height: 21px;
        text-align: center;
        letter-spacing: -0.138462px;
        color: $primaryColor1;

        &:not(:last-child) {
          margin-bottom: 24px;
        }
      }
    }
  }
}
</style>
