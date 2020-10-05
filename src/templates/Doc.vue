<template>
  <Layout>
    <h1>
      {{ $page.doc.title }}
    </h1>
    <div class="markdown" v-html="$page.doc.content" />
    <footer>
      <div class="footer-inner" id="footer-left">
        <ul>
          <li id="footer-year">2020</li>
        </ul>
      </div>
      <div class="footer-inner" id="footer-right">
        <ul>
          <li id="twitter">
            <a href="https://twitter.com/numberatomism">@numberatomism</a>
          </li>
          <li id="email">
            <a href="mailto: ayakowenko@gmail.com">ayakowenko@gmail.com</a>
          </li>
        </ul>
      </div>
    </footer>
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
*/

/deep/ > h2 {
  padding-top: 100px;
  margin-top: -80px;

  @include respond-above(md) {
    font-size: 1.8rem;
  }
}

/deep/ > p > img {
  max-width: 100%;
}

.markdown {
  padding-bottom: 40px;
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

@include respond-between(xxs, md) {
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
