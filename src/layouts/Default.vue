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
      <footer>
        <div class="footer-inner" id="footer-left">
          <ul>
            <li id="footer-year">2020</li>
          </ul>
        </div>
        <div class="footer-inner" id="footer-right">
          <ul>
            <li id="facebook">Twitter</li>
            <li id="instagram">Email</li>
          </ul>
        </div>
      </footer>
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
        navigator.serviceWorker.register("/sw.js").then(function () {
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
  @import url("https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:ital,wght@0,200;0,300;0,400;1,200;1,300;1,400&display=swap");

  padding: 140px 160px 20px 120px;
  transition: transform 0.15s ease-in-out;

  @include respond-between(xxs, xs) {
    padding: 100px 80px 100px 80px;
  }

  @include respond-between(xs, sm) {
    padding: 100px 80px 100px 80px;
  }

  @include respond-between(sm, md) {
    padding: 100px 60px 100px 20px;
    transform: translateX(280px);
    width: calc(100% - 280px);
  }

  @include respond-between(md, lg) {
    padding: 140px 160px 100px 20px;
    transform: translateX(280px);
    width: calc(100% - 280px);
  }

  @include respond-above(lg) {
    padding: 140px 160px 100px 120px;
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
    background: linear-gradient(260deg, #8fea93, #51c574);
  }

  &--sidebar-is-open {
    transform: translate(280px);
  }

  .flex-item a {
    background: white;
    -webkit-background-clip: content-box;
    background-clip: content-box;
    -webkit-text-fill-color: white;
    -webkit-box-decoration-break: clone;
    box-decoration-break: clone;
    background-color: transparent;
    font-weight: 600;
  }
}

footer {
  margin: 0;
  padding: 0;
  width: 100%;
  display: flex;
  justify-content: space-between;
  //box-sizing: border-box;
  border-top: 1px solid $textBright;
}

.footer-inner {
  background: transparent;
  width: 50%;
  display: flex;
  align-items: center;
  padding: 0;
  color: $textBright;
}

#footer-left {
  display: flex;
  //justify-content: flex-end;
}

#footer-left ul {
  display: flex;
  list-style-type: none;
  //justify-content: flex-end;
  padding-inline-start: 0px;
}

#footer-left ul li {
  padding: 0px 20px;
  color: $textBright;
}

#footer-right {
  display: flex;
  justify-content: flex-end;
}

#footer-right ul {
  display: flex;
  list-style-type: none;
  justify-content: flex-end;
  padding-inline-start: 0px;
}

#footer-right ul li {
  padding: 0px 20px;
  color: $textBright;
}

@media screen and (max-width: 576px) {
  footer {
    flex-direction: column;
    align-items: center;
  }
  .footer-inner {
    justify-content: center;
    min-width: 240px;
  }
  #footer-right {
    justify-content: center;
  }
  #footerright ul {
    justify-content: center;
  }
}
</style>
