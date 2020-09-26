<template>
  <div class="site">
    <Header :menuToggle="sidebar" />
    <Sidebar v-if="sidebar" />
    <main class="main" :class="{'main--no-sidebar': !sidebar, 'main--sidebar-is-open' : this.$store.state.sidebarOpen}">
      <slot/>
    </main>
  </div>
</template>

<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>

<script>
import Header from '~/components/Header.vue'
import Sidebar from '~/components/Sidebar.vue'

export default {
  components: {
    Header,
    Sidebar
  },
  props: {
    sidebar: {
      type: Boolean,
      default: true
    }
  },
  mounted() {
    this.$store.commit('closeSidebar')
    if (process.isClient) {
      if('serviceWorker' in navigator) {
        navigator.serviceWorker
          .register('/sw.js')
          .then(function() { console.log("Service Worker Registered"); });
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.site {
  overflow: hidden;
}

.main {
  padding: 140px 160px 20px 120px;
  transition: transform .15s ease-in-out;

  @include respond-between(xxs, xs) {
    padding: 100px 88px 100px 88px;
  }

  @include respond-between(xs, sm) {
    padding: 100px 88px 100px 88px;
  }
  
  @include respond-between(sm, md) {
    padding: 100px 60px 20px 20px;
    transform: translateX(300px);
    width: calc(100% - 300px);
  }

  @include respond-between(md, lg) {
    padding: 140px 160px 20px 120px;
    transform: translateX(300px);
    width: calc(100% - 300px);
  }

  &--no-sidebar {
    transform: translate(0);
    margin: 0 auto;
    width: 100%;
    max-width: 1400px;
  }

  &--sidebar-is-open {
    transform: translate(300px);
  }
}
</style>
