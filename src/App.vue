<template>
  <div id="app">
    <!-- Taken from the Fundament documentation -->
    <div
      class="wrapper-fluid wrapper-navbar sticky-navbar"
      id="wrapper-navbar"
      itemscope=""
      itemtype="http://schema.org/WebSite"
    >
      <a class="skip-link screen-reader-text sr-only" href="#content">Skip to content</a>
      <nav class="navbar navbar-expand-lg navbar-light">
        <div class="container">
          <!-- Your site title as branding in the menu -->
          <a href="#" class="navbar-brand custom-logo-link" rel="home" itemprop="url"
            ><img
              src="https://fundament.acdh.oeaw.ac.at/common-assets/images/acdh_logo.svg"
              class="img-fluid"
              alt="ACDH Logo"
              itemprop="logo"
          /></a>
          <a class="navbar-brand site-title-with-logo" rel="home" href="#" title="MMP Search" itemprop="url">
            MMP Search
          </a>
          <!-- .collapse navbar-collapse -->
        </div>
        <!-- .container -->
      </nav>
      <!-- .site-navigation -->
    </div>

    <Search></Search>
  </div>
</template>

<script>
import Search from "./components/Search.vue";
export default {
  name: "App",
  components: { Search },
};
</script>

<style>
#app {
  width: 100%;
}
</style>
