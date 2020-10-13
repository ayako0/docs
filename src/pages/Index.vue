<template>
  <Layout :sidebar="false">
    <div class="flex-container">
      <div class="flex-item"></div>
      <div class="flex-item">
        <h2>Benjamin Graham Equation</h2>
        <p>Does Benjamin Graham's equation outperform the market?</p>
        <a href="/benjamin-graham">Learn more</a>
      </div>
      <div class="flex-item">
        <h2>Equity per Share Growth</h2>
        <p>One of the leading factors in correlation to the S&P 500.</p>
        <a href="/earnings-ratios#equity-per-share-growth">Learn more</a>
      </div>
      <div class="flex-item">
        <h2>Quick Ratio</h2>
        <p>A factor that performs in consistency with the S&P 500.</p>
        <a href="/operation-ratios#quick-ratio">Learn more</a>
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
      description: "Home",
    };
  },
  metaInfo() {
    return {
      title: this.description,
      meta: [
        {
          key: "description",
          name: "description",
          content: "Visualizing economic theory.",
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
  line-height: 1.4;
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
  height: 100%;
}
.flex-item {
  color: white;
}
.flex-item:nth-child(1) {
  order: 0;
  flex: 12 1 auto;
  align-self: auto;
  margin-top: auto;
  width: 33.4%;
}
.flex-item:nth-child(2),
.flex-item:nth-child(3),
.flex-item:nth-child(4) {
  order: 0;
  flex: 1 1 auto;
  align-self: auto;
  transform: translateY(50%);
  width: 22.2%;
  padding-right: 20px;
  // font-family: "IBM Plex Sans", monospace;
  // font-size: 14px;
  // font-style: italic;
}
.main .flex-item a {
  text-decoration: none;
}

@include respond-below(sm) {
  .flex-container {
    padding: 0px 80px;
  }
}

@include respond-between(xxs, sm) {
  .flex-container {
    flex-direction: column;
    height: 100%;
    width: 100%;
    padding: 0px 160px;
    flex-direction: column;
    justify-content: space-between;
  }
  .flex-item:nth-child(1) {
    display: none;
  }
  .flex-item:nth-child(2),
  .flex-item:nth-child(3),
  .flex-item:nth-child(4) {
    width: 100%;
    padding-right: 0px;
    transform: translateY(0);
    margin-top: 80px;
  }
  .flex-item:nth-child(4) {
    padding-bottom: 100px;
  }
}
@include respond-between(sm, md) {
  .flex-item:nth-child(1) {
    width: 20%;
  }
  .flex-item:nth-child(2),
  .flex-item:nth-child(3),
  .flex-item:nth-child(4) {
    width: 26.7%;
  }
}
</style>
