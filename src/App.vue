<template>
  <div id="app">
    <!--Wrapper for sticky footer-->
    <div id='sticky-footer'>
      <!--The app loading-->
      <app-loading></app-loading>

      <!--The app notification-->
      <app-notification></app-notification>

      <!--The app header-->
      <app-header>
<!--         <img slot='icon' src="./assets/logo.png" width='30px'> -->
      </app-header>

      <!--Main app navigation-->
      <app-navbar></app-navbar>

      <!--This is where the content of the page goes to-->
      <app-body>
        <!--The router view will render the page component based on the path-->
        <transition
          :name='transitionName'
          :mode='transitionMode'>
          <router-view></router-view>
        </transition>
      </app-body>
    </div>
    <!--Sticky footer-->
    <app-footer></app-footer>
  </div>
</template>

<script>
import AppHeader from './components/atom/app-header'
import AppNavbar from './components/atom/app-navbar'
import AppBody from './components/atom/app-body'
import AppFooter from './components/atom/app-footer'
import AppNotification from './components/atom/app-notification'
import AppLoading from './components/atom/app-loading'

export default {
  name: 'app',
  components: {
    AppHeader,
    AppNavbar,
    AppBody,
    AppFooter,
    AppNotification,
    AppLoading
  },
  data () {
    return {
      transitionName: 'slideLeft',
      transitionMode: 'out-in',
      name: this.name
    }
  },
  watch: {
    '$route' (to, from) {
      this.name = this.$route.name
      const toDepth = to.path.split('/').length
      const fromDepth = from.path.split('/').length
      this.transitionName = toDepth < fromDepth ? 'slideRight' : 'slideLeft'
    }
  }
}
</script>

<style lang='scss'>
@import './styles/colors.scss';
@import './styles/reset.css';
@import './styles/box-sizing.css';
@import './styles/grid-layout.css';
@import './styles/typography.scss';
@import './styles/vue-animate.min.css';

body.disable-hover {
  pointer-events: none;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
#sticky-footer {
  /*
   * For sticky footer, offset the footer height
  **/
  margin-bottom: -50px;
  height: 100%;
  min-height: 100vh;
}
#sticky-footer:after {
  content: '';
  display: block;
  /*
   * Whereby the 100px is the offsetted height for the footer
  **/
  height: 50px;
}

</style>
