<template>
  <no-ssr>
     
  <nav class="navbar has-shadow">
    <div class="container">
      <div class="navbar-brand">
        <a class="navbar-item">
          <nuxt-link to="/">
            <img src="~/assets/images/logo2.png">
          </nuxt-link>
        </a>
        <div class="navbar-burger burger" data-target="navbarDropdown" @click="menuIsActive = !menuIsActive" :class="{ 'is-active': menuIsActive }">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </div>
      <div id="navbarDropdown" class="navbar-menu" :class="{ 'is-active': menuIsActive }">
        <div class="navbar-start">
          <div class="navbar-item has-dropdown is-hoverable">
            <a class="navbar-link" href="">
              Resources
            </a>
            <div class="navbar-dropdown is-boxed">
              <a class="navbar-item" href="">
                Education
              </a>
              <a class="navbar-item" href="">
                Four Year Plan
              </a>
              <a class="navbar-item" href="">
                 <nuxt-link to="opportunities">Opportunities</nuxt-link>
              </a>
              <a class="navbar-item" href="">
                 <nuxt-link to="jobs">Jobs</nuxt-link>
              </a>
              <a class="navbar-item" href="">
                Careers
              </a>
              <a class="navbar-item" href="">
                <nuxt-link to="faculty">Faculty</nuxt-link>
              </a> 
            </div>
          </div>
          <div class="navbar-item has-dropdown is-hoverable">
            <a class="navbar-link" href="">
              Get Involved
            </a>
            <div class="navbar-dropdown is-boxed">
              <a class="navbar-item" href="">
                Events
              </a>
              <a class="navbar-item" href="">
                Outreach
              </a>
              <a class="navbar-item" href="" >
                <nuxt-link to="podcast">Podcast</nuxt-link>
              </a>
              <a class="navbar-item" href="">
                Sponsorship
              </a>
              <a class="navbar-item" href="">
                <nuxt-link to="shop">Shop</nuxt-link>
              </a>
              <hr class="navbar-divider">
              <a class="navbar-item" href="">
                <nuxt-link to="calendar">Calendar</nuxt-link>
              </a>
              <a class="navbar-item" href="">
                <nuxt-link to="contact">Contact</nuxt-link>
              </a>
            </div>
          </div>
        </div>
        <div class="navbar-end">
          <div class="navbar-item">
            <p v-if="$auth.loggedIn"> Hi there, {{$auth.user.name.split(" ")[0]}}! </p>
          </div>
          <div class="navbar-item">

            <div class="field is-grouped">

              <p class="control">
                <a class="button" v-if="$auth.loggedIn" @click="logout()">
                  <span class="icon">
                    <i class="fas fa-sign-in-alt"/>
                  </span>
                  <span>

                    <nuxt-link to="/" >Logout</nuxt-link>
                  </span>
                </a>
                <a class="button" v-else>
                  <span class="icon">
                    <i class="fas fa-sign-in-alt"/>
                  </span>
                  <span>
                    <nuxt-link to="login">Login</nuxt-link>
                  </span>
                </a>
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>

</no-ssr>

</template>

<script>
export default {
  data: function() {
    return {
      menuIsActive: false
    }
  }, 
  methods: {
    toggleMenu: function() {
      console.log("Yessir");
      this.menuIsActive = !this.menuIsActive;
    },
    logout: function() {
      console.log("Pre logout, member:" + this.$auth.$storage.getCookie("member"));
      this.$auth.$storage.setCookie("member", "false", true);
      console.log("Post logout, member:" + this.$auth.$storage.getCookie("member"));
      this.$auth.logout();
    }
  },
   watch: {
    '$route' () {
      this.menuIsActive = false;
    }
  }
}

</script>

<style lang="scss" scoped>

a {
  color: #337A8A;
}

.navbar-link:hover {
  color: #D58521;
}

.navbar-link:after {
  border-color: #D58521;
}

.navbar {
  height: 3.25rem;
}

.navbar-item {
  color: #0a0a0a !important;
}

img {
  display: flex;
  background-size: 80%;
}
</style>

