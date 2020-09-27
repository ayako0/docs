<template>
  <Layout :sidebar="false">
    <div class="flex-container">
      <div class="flex-item">
        <p>&#9632;</p>
      </div>
      <div class="flex-item">
        <a href="/getting-started">Featured link 1</a>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
          eiusmod tempor...
        </p>
      </div>
      <div class="flex-item">
        <a href="/getting-started">Featured link 2</a>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
          eiusmod tempor...
        </p>
      </div>
      <div class="flex-item">
        <a href="/getting-started">Featured link 3</a>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
          eiusmod tempor...
        </p>
      </div>
    </div>
  </Layout>
</template>

<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>

<script>
import GitLink from "~/components/GitLink.vue";
import Shortcut from "~/components/Shortcut.vue";

export default {
  components: {
    GitLink,
    Shortcut,
  },
  data() {
    return {
      description:
        "The ultimate static generated documentation theme for the JAM-stack",
    };
  },
  metaInfo() {
    return {
      title: this.description,
      meta: [
        {
          key: "description",
          name: "description",
          content:
            "A theme for static site documentation based on Gridsome, ready to deploy to Netlify in one click.",
        },
      ],
    };
  },
};
</script>

<style lang="scss" scoped>
.content {
  display: flex;
  flex-direction: column;
}

h1 {
  text-align: center;
  max-width: 600px;
  margin: 1.5em auto 1.5em;

  @include respond-above(md) {
    max-width: 1000px;
  }
}

h2 {
  font-size: 1.4rem;
  margin: 0;
}

nav {
  display: flex;
  justify-content: space-between;
  flex-direction: column;

  @include respond-above(sm) {
    flex-direction: row;
  }
}

.git {
  margin: 3em 0 0;
  align-self: center;

  @include respond-above(md) {
    margin: 5em 0 0;
  }
}

.flex-container {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: flex-start;
  align-content: stretch;
  // align-items: flex-end;
  height: 100%;
  // font-family: "IBM Plex Sans", monospace;
  // font-size: 14px;
  // font-style: italic;
}

.flex-item {
  color: white;
  font-style: italic;
}

.flex-item:nth-child(1) {
  order: 0;
  flex: 12 1 auto;
  align-self: auto;
  margin-top: auto;
  width: 50%;
}

.flex-item:nth-child(2) {
  order: 0;
  flex: 1 1 auto;
  align-self: auto;
  transform: translateY(50%);
}

.flex-item:nth-child(3) {
  order: 0;
  flex: 1 1 auto;
  align-self: auto;
  transform: translateY(50%);
}

.flex-item:nth-child(4) {
  order: 0;
  flex: 1 1 auto;
  align-self: auto;
  transform: translateY(50%);
}

.flex-item:nth-child(2),
.flex-item:nth-child(3),
.flex-item:nth-child(4) {
  width: 16.67%;
}
</style>
