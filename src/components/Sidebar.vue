<template>
  <aside
    class="sidebar disable-scrollbars"
    :class="{ 'sidebar--open': this.$store.state.sidebarOpen }"
  >
    <nav>
      <ul>
        <li
          class="section"
          v-for="{ node } in $static.menu.edges"
          :key="node.id"
        >
          <h3 class="section-title">{{ node.section }}</h3>
          <ul>
            <li v-for="item in node.topics" :key="item.title">
              <g-link class="topic" :to="'/' + item.slug">{{
                item.title
              }}</g-link>
              <ul
                v-if="checkAnchors(node.slug, item.slug)"
                v-for="{ node } in $static.docs.edges"
                :key="node.id"
              >
                <li v-for="heading in node.headings" :key="heading.value">
                  <a
                    class="sub-topic"
                    :href="'/' + item.slug + heading.anchor"
                    >{{ heading.value }}</a
                  >
                </li>
              </ul>
            </li>
          </ul>
        </li>
      </ul>
    </nav>
  </aside>
</template>

<static-query>
query Menu {
  menu: allMenu(order:ASC) {
    edges {
      node {
        section
        topics {
          title
          slug
        }
      }
    }
  }
  docs: allDoc {
    edges {
      node {
        slug
        headings {
          value
          anchor
        }
      }
    }
  }
}
</static-query>

<script>
import GitLink from "~/components/GitLink.vue";
import throttle from "lodash/throttle";

export default {
  components: {
    GitLink,
  },
  watch: {
    $route() {
      this.$store.commit("closeSidebar");
    },
  },
  methods: {
    checkAnchors(slug, item) {
      if (slug == item) {
        return true;
      }
    },
    stateFromSize: function () {
      if (
        window.getComputedStyle(document.body, ":before").content == '"small"'
      ) {
        this.$store.commit("closeSidebar");
      } else {
        this.$store.commit("openSidebar");
      }
    },
    sidebarScroll: function () {
      let mainNavLinks = document.querySelectorAll(
        ".topic.active + ul .sub-topic"
      );
      let fromTop = window.scrollY;

      mainNavLinks.forEach((link) => {
        let section = document.querySelector(link.hash);
        let allCurrent = document.querySelectorAll(".current"),
          i;

        if (section.offsetTop <= fromTop) {
          for (i = 0; i < allCurrent.length; ++i) {
            allCurrent[i].classList.remove("current");
          }
          link.classList.add("current");
        } else {
          link.classList.remove("current");
        }
      });
    },
  },
  beforeMount() {
    this.stateFromSize();
  },
  mounted() {
    window.addEventListener("scroll", throttle(this.sidebarScroll, 50));
  },
};
</script>

<style lang="scss" scoped>
.sidebar {
  transition: background 0.15s ease-in-out, transform 0.15s ease-in-out,
    border-color 0.15s linear;
  padding: 140px 0px 100px 80px;
  width: 280px;
  line-height: 20px;
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  z-index: 9;
  will-change: transform;
  transform: translateX(-280px);
  overflow: auto;
  text-align: right;

  @include respond-above(sm) {
    transform: translateX(0);
  }

  &--open {
    transform: translateX(0);
  }

  .dark & {
    background: $sidebarDark;
    border-color: shade($sidebarDark, 40%);
  }
}

nav {
  position: relative;
  min-height: 100%;
  padding-bottom: 40px;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;

  a {
    text-decoration: none;
    color: inherit;
    padding: 5px 0;
    display: block;

    &.active {
      background: linear-gradient(260deg, #1aff24, #20e95c);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      -webkit-box-decoration-break: clone;
      opacity: 1;
    }
  }
}

.section {
  margin-bottom: 30px;
}

.section-title {
  font-size: 1rem;
  font-weight: 400;
  margin: 0;
  padding-bottom: 5px;
  margin-top: 4em;
}

.topic {
  font-weight: 600;
  font-size: 1rem;
  border-top: 1px solid $textBright;
  margin-top: 1em;
  margin-left: 50%;
  width: 50%;
  font-family: -apple-system,BlinkMacSystemFont,Segoe UI,Helvetica,Arial,sans-serif,Apple Color Emoji,Segoe UI Emoji;
}

.sub-topic {
  font-size: 1rem;
  position: relative;
  font-weight: 600;

  &.current {
    &::after {
      opacity: 1;
      content: "";
      transition: opacity 0.15s ease-in-out;
      width: 40px;
      height: 4px;
      background: linear-gradient(260deg, #1aff24, #20e95c);
      display: block;
      position: absolute;
      z-index: -1;
      left: -60px;
      top: 15px;
    }
  }
}

.git {
  position: absolute;
  bottom: 0;
  left: 0;
}

.disable-scrollbars {
  scrollbar-width: none; /* Firefox */
  -ms-overflow-style: none; /* IE 10+ */
}

.disable-scrollbars::-webkit-scrollbar {
  width: 0px;
  background: transparent; /* Chrome/Safari/Webkit */
}
</style>
