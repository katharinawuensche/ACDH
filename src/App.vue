<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light">
      <div class="container">
        <!-- Your site title as branding in the menu -->
        <a href="#" class="navbar-brand custom-logo-link" rel="home" itemprop="url"
          ><img src="./assets/logo.png" class="img-fluid" alt="Your Logo" itemprop="logo"
        /></a>
        <a class="navbar-brand site-title-with-logo" rel="home" href="#" title="Your Project" itemprop="url"
          >Your Project</a
        >
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
    <img alt="Vue logo" src="./assets/logo.png" width="25%" />
    <HelloWorld msg="Hello Vue in CodeSandbox!" />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld";

export default {
  name: "App",
  components: {
    HelloWorld,
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
  width: 100%;
}
</style>
