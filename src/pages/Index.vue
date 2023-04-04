<template>
  <Layout :sidebar="false">
    <main class="relative">
      <section class="bg-silver">
        <div class="container p2 border-box" style="padding-bottom: 0">
          <!--div class="container p2 border-box" style="padding-top: 7.5vh"-->
          <div
            class="md-col-12 p3 border-box inline-block align-middle"
            style="padding-bottom: 0"
          >
            <h1 class="h0 mt0 mb2">Quant</h1>

            <div class="clearfix mb2">
              <div class="relative mb2 ml0 md-col md-col-4">
                <div class="border-box mt2 mb2">
                  <h4 class="mt0 mb0 i2">29,923.07%</h4>
                  <a href="/trading-algorithm#personal-chart" class="mb0 mt0 i1"
                    >Optimized Momentum <br />Trading →</a
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="container p2 border-box">
          <!--div class="container p2 border-box" style="padding-top: 7.5vh"-->
          <div class="md-col-12 p3 border-box inline-block align-middle">
            <h1 class="h0 mt0 mb2">Fundamentals</h1>

            <div class="clearfix mb2">
              <div class="relative mb2 ml0 md-col md-col-4 md-border-right">
                <div class="border-box mt2 mb2">
                  <h4 class="mt0 mb0 i2">High: 946.69%</h4>
                  <a
                    href="/earnings-ratios#equity-per-share-growth"
                    class="mb0 mt0 i1"
                    >Equity per <br />Share Growth →</a
                  >
                </div>
              </div>

              <div
                class="relative mb2 md-col md-col-4 md-center md-border-right"
              >
                <div class="border-box mt2 mb2">
                  <h4 class="mt0 mb0 i2">High: 1,270.05%</h4>
                  <a
                    href="/valuation-ratios#price-to-sales-ratio"
                    class="mb0 mt0 i1"
                    >Price to<br />
                    Sales Ratio →</a
                  >
                </div>
              </div>

              <div class="relative mb2 mr0 md-col md-col-4 md-right-align">
                <div class="border-box mt2 mb2">
                  <h4 class="mt0 mb0 i2">Low: -91.3%</h4>
                  <a
                    href="/earnings-report#earnings-per-share-eps"
                    class="mb0 mt0 i1"
                    >Earnings <br />per Share →</a
                  >
                </div>
              </div>
            </div>
            <div class="clearfix mb2">
              <p class="mb0 italic muted p1">
                Historical fundamental data from Jan 2nd, 2006 to Sep 1st, 2020.
                Quantopian fundamentals aggregated quarterly. Quantopian shut
                down Nov 2020: Zipline was used in production as its backtesting
                and live trading engine, to which most code can be converted.
              </p>
            </div>
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
          content: "Quantitative algorithms and technical projects.",
        },
      ],
    };
  },
};
</script>

<style lang="scss" scoped></style>
