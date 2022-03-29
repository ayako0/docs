<template>
  <div class="site">
    <Header :menuToggle="sidebar" />
    <Sidebar v-if="sidebar" />
    <main
      class="main"
      :class="{
        'main--no-sidebar': !sidebar,
        'main--sidebar-is-open': this.$store.state.sidebarOpen,
      }"
    >
      <slot />
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
import Header from "~/components/Header.vue";
import Sidebar from "~/components/Sidebar.vue";

export default {
  components: {
    Header,
    Sidebar,
  },
  props: {
    sidebar: {
      type: Boolean,
      default: true,
    },
  },
  mounted() {
    this.$store.commit("closeSidebar");
    if (process.isClient) {
      if ("serviceWorker" in navigator) {
        navigator.serviceWorker.register("/sw.js").then(function() {
          console.log("Service Worker Registered");
        });
      }
    }
  },
};
</script>

<style lang="scss" scoped>
.site {
  overflow: hidden;
}

.main {
  padding: 140px 40px 20px 40px;
  transition: transform 0.15s ease-in-out;

  @include respond-below(xxs) {
    padding: 140px 20px 100px 20px;

    &--no-sidebar {
      overflow: scroll;
    }
  }

  @include respond-between(xxs, xs) {
    padding: 140px 20px 100px 20px;
    &--no-sidebar {
      overflow: scroll;
    }
  }

  @include respond-between(xs, sm) {
    padding: 140px 20px 100px 20px;
    &--no-sidebar {
      overflow: scroll;
    }
  }

  @include respond-between(sm, md) {
    padding: 140px 40px 100px 40px;
    transform: translateX(280px);
    width: calc(100% - 280px);
  }

  @include respond-between(md, lg) {
    padding: 140px 40px 100px 40px;
    transform: translateX(280px);
    width: calc(100% - 280px);
  }

  @include respond-above(lg) {
    padding: 140px 40px 100px 40px;
    transform: translateX(280px);
    width: calc(100% - 280px);
  }

  &--no-sidebar {
    transform: translate(0);
    -webkit-transform: translate(0);
    transform: translate(0);
    width: 100%;
    max-width: 100%;
    height: 100vh;
    padding: 20px;
    background: #f1f1f1;
  }

  &--sidebar-is-open {
    transform: translate(280px);
  }
}
</style>
