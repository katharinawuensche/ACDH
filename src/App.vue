<template>
  <div id="app">
    <!-- Taken from the Fundament documentation -->
    <nav class="navbar navbar-expand-lg navbar-light">
      <div class="container">
        <!-- Your site title as branding in the menu -->
        <a href="#" class="navbar-brand custom-logo-link" rel="home" itemprop="url"
          ><img src="./assets/logo.png" class="img-fluid" alt="Your Logo" itemprop="logo"
        /></a>
        <a class="navbar-brand site-title-with-logo" rel="home" href="#" title="MMP Search" itemprop="url">
          MMP Search
        </a>
        <button
          class="navbar-toggler"
          type="button"
          data-toggle="collapse"
          data-target="#navbarNavDropdown"
          aria-controls="navbarNavDropdown"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse justify-content-end" id="navbarNavDropdown">
          <!-- The Menu goes here -->
          <ul id="main-menu" class="navbar-nav">
            <li id="menu-item-11" class="menu-item nav-item"><a title="Home" href="#" class="nav-link">Home</a></li>
            <li id="menu-item-15" class="menu-item nav-item"><a title="About" href="#" class="nav-link">About</a></li>
          </ul>
        </div>
        <!-- .collapse navbar-collapse -->
      </div>
      <!-- .container -->
    </nav>
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
