<template>
  <header class="navbar">
    <router-link to="/home">
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
  </header>
</template>

<script>
import { mapState } from 'vuex'

export default {
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

  .links {
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
}
</style>
