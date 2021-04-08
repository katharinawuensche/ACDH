<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light">
      <div class="container">
        <!-- Your site title as branding in the menu -->
        <a href="#" class="navbar-brand custom-logo-link" rel="home" itemprop="url"
          ><img src="./assets/logo.png" class="img-fluid" alt="Your Logo" itemprop="logo"
        /></a>
        <a class="navbar-brand site-title-with-logo" rel="home" href="#" title="MMP Search" itemprop="url"
          >MMP Search</a
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
          <form class="form-inline my-2 my-lg-0 navbar-search-form" method="get" action="/" role="search">
            <input
              class="form-control navbar-search"
              id="s"
              name="s"
              type="text"
              placeholder="Search"
              value=""
              autocomplete="off"
            />
            <button type="submit" class="navbar-search-icon">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
                class="feather feather-search"
              >
                <circle cx="11" cy="11" r="8"></circle>
                <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
              </svg>
            </button>
          </form>
        </div>
        <!-- .collapse navbar-collapse -->
      </div>
      <!-- .container -->
    </nav>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
};
</script>

<style>
#app {
  width: 100%;
}
</style>
