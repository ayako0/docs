<template>
  <Layout :sidebar="false">
    <main class="relative">
      <section class="bg-silver">
        <div
          class="container p2 border-box"
          style="padding-top: 7.5rem; padding-bottom: 9.5rem;"
        >
          <div class="md-col-12 p2 border-box inline-block align-middle">
            <h1 class="h0 mt0 mb2">Fundamentals</h1>

            <div class="clearfix mb2">
              <div class="relative mb2 ml0 md-col md-col-4 md-border-right">
                <div class="border-box mt2 mb2">
                  <h3 class="mt0 mb0 h2">29,923.07%</h3>
                  <a href="/trading-algorithm#personal-chart" class="mb0 mt0 a1"
                    >Markowitz <br />Optimization →</a
                  >
                </div>
              </div>

              <div
                class="relative mb2 md-col md-col-4 md-center md-border-right"
              >
                <div class="border-box mt2 mb2">
                  <h3 class="mt0 mb0 h2">1270.05%</h3>
                  <a
                    href="/valuation-ratios#price-to-sales-ratio"
                    class="mb0 mt0 a1"
                    >Price to<br />
                    Sales Ratio →</a
                  >
                </div>
              </div>

              <div class="relative mb2 mr0 md-col md-col-4 md-right-align">
                <div class="border-box mt2 mb2">
                  <h3 class="mt0 mb0 h2">-91.3%</h3>
                  <a
                    href="/earnings-report#earnings-per-share-eps"
                    class="mb0 mt0 a1"
                    >Earnings <br />per Share →</a
                  >
                </div>
              </div>
            </div>

            <p class="mb0 italic muted p1">
              Historical fundamental data from Jan 2nd, 2006 to Sep 1st, 2020 |
              Future research TBD
            </p>
          </div>
        </div>
      </section>
    </main>
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
//.bg-silver {
//  background-color: none;
//}
</style>
