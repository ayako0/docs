<template>
  <header class="header" :class="{ 'header--scrolled': pageScrolled }">
    <Logo :color="logoColor" />
    <div class="menu-left"><MenuToggle v-if="menuToggle" /></div>
    <nav class="nav">
      <ThemeSwitch v-off:theme-change="updateLogo" />
    </nav>
  </header>
</template>

<script>
import ThemeSwitch from "~/components/ThemeSwitch.vue";
import MenuToggle from "~/components/MenuToggle.vue";
import Logo from "~/components/Logo.vue";
import throttle from "lodash/throttle";

export default {
  components: {
    ThemeSwitch,
    MenuToggle,
    Logo,
  },
  props: {
    menuToggle: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return {
      pageScrolled: false,
      logoColor: "bright",
    };
  },
  methods: {
    updateLogo: function() {
      this.logoColor = this.logoColor == "bright";
    },
    headerScroll: function() {
      let fromTop = window.scrollY;

      if (
        (fromTop > 40 && this.pageScrolled == false) ||
        (fromTop <= 40 && this.pageScrolled == true)
      ) {
        this.pageScrolled = !this.pageScrolled;
      }
    },
  },
  mounted() {
    window.addEventListener("scroll", this.headerScroll);

    if (process.isClient) {
      this.logoColor = localStorage.getItem("theme");
    }
  },
};
</script>

<style lang="scss" scoped>
.menu-left {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 10;
  margin: 20px;
  transition: padding 0.15s linear, background 0.15s linear,
    border-color 0.15s linear;
}

.header {
  display: flex;
  //justify-content: space-between;
  //align-items: center;
  position: fixed;
  bottom: 0;
  //right: -12px;
  left: 0;
  z-index: 10;
  margin: 1.25rem;
  transition: padding 0.15s linear, background 0.15s linear,
    border-color 0.15s linear;
  //will-change: padding, background;
  //max-width: 100%;

  @include respond-above(sm) {
    margin: 1.25rem;
  }

  &--scrolled {
    @include respond-below(sm) {
      margin: 1.25rem 1.25rem;

      .dark & {
        background: $sidebarDark;
        border-color: shade($sidebarDark, 40%);
      }

      .bright & {
        background: $sidebarBright;
        border-color: shade($sidebarBright, 10%);
      }
    }
  }
}

nav {
  display: flex;
  // display: none;
}
</style>
