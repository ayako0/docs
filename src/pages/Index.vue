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
                    href="/earnings-ratios#equity-per-share-growth"
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

            <p class="mb0 italic muted">
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
.container {
  max-width: 76pc;
  max-width: 76rem;
  margin-left: auto;
  margin-right: auto;
}
.p2 {
  //padding: 1pc;
  padding: 30px;
}
.border-box {
  box-sizing: border-box;
}
.md-col-12 {
  width: 100%;
}
.inline-block {
  display: inline-block;
}
.align-middle {
  vertical-align: middle;
}
.h0,
.h-lg {
  font-size: 44px;
  font-size: 2.75rem;
  letter-spacing: -1px;
  letter-spacing: -0.08rem;
}
@include respond-above(sm) {
  .h0 {
    font-size: 3.25rem;
  }
  .h-lg {
    font-size: 5rem;
  }
  .h1,
  h1 {
    font-size: 2.5rem;
  }
}
@include respond-above(md) {
  .h0 {
    font-size: 4rem;
  }
  .h-lg {
    font-size: 6.25rem;
  }
}
.clearfix:after,
.clearfix:before {
  content: " ";
  display: table;
}
.clearfix:after {
  clear: both;
}
@include respond-above(sm) {
  .md-col {
    float: left;
    box-sizing: border-box;
  }
  .md-col-4 {
    width: 33.33333%;
  }
  .md-border-right {
    border-right-style: solid;
    border-right-width: 1px;
    border-right-color: rgba(43, 44, 48, 0.125);
  }
  .md-center {
    text-align: center;
  }
  .md-right-align {
    text-align: right;
  }
}
@include respond-below(sm) {
  .h0 {
    font-size: 1.875rem;
  }
}

.ml0 {
  margin-left: 0;
}
.mt2 {
  margin-top: 1pc;
  margin-top: 1rem;
}
.mb2 {
  margin-bottom: 1pc;
  margin-bottom: 1rem;
}
.mt0 {
  margin-top: 0;
}
.mb0 {
  margin-bottom: 0;
}
.h2 {
  font-size: 26px;
  font-size: 1.625rem;
}
.mr0 {
  margin-right: 0;
}
.italic {
  font-style: italic;
}
.muted {
  opacity: 0.5;
}
.a1 {
  font-size: 1.125rem;
}
</style>
