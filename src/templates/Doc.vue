<template>
  <Layout>
    <!--h1>
      {{ $page.doc.title }}
    </h1-->
    <div class="markdown" v-html="$page.doc.content" />

    <div class="clearfix bt">
      <div class="relative ml0 md-col md-col-3 ft footer-heading">
        <div class="border-box">
          <p class="mt0 mb0">2020 -</p>
        </div>
      </div>
      <div class="relative ml0 md-col md-col-3 md-right-align ft">
        <div class="border-box">
          <a href="https://donate.stripe.com/bIYfZ56ICevG8Fy000">Donate</a>
        </div>
      </div>

      <div class="relative md-col md-col-3 md-center md-right-align ft">
        <div class="border-box">
          <p class="mt0 mb0">Social</p>
          <a href="https://x.com/numberatomism">X</a>
          <a href="https://github.com/ayako0">Github</a>
        </div>
      </div>

      <div class="relative mr0 md-col md-col-3 md-right-align ft">
        <div class="border-box">
          <a href="mailto:ayakowenko@protonmail.com">Email</a>
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query Doc ($path: String!) {
  doc: doc (path: $path) {
    title
    path
    timeToRead
    content
  }
}
</page-query>

<script>
export default {
  metaInfo() {
    return {
      title: this.$page.doc.title,
      meta: [
        {
          key: "description",
          name: "description",
          content: this.$page.doc.description,
        },
      ],
    };
  },
};
</script>

<style lang="scss" scoped>
/*
/deep/ > p {
  opacity: .8;
}

/deep/ > h2 {
  padding-top: 6.25rem;
  margin-top: -5rem;

  @include respond-above(md) {
    font-size: 1.75rem;
  }
}

/deep/ > p > img {
  max-width: 100%;
}
*/

.markdown {
  padding-bottom: 2.5rem;
}
</style>
