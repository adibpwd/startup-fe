<template>
    <header class="flex items-center">
      <div style="height: 54px" class="pr-5">
        <img src="/logo.svg" alt="logo" class="h-full" />
      </div>
      <ul class="flex items-center">
        <li>
          <nuxt-link class="text-white hover:text-teal-500 text-lg px-4 py-3" to="/">Home</nuxt-link>
        </li>
        <li>
          <nuxt-link class="text-white hover:text-teal-500 text-lg px-4 py-3" to="#">Project</nuxt-link>
        </li>
        <li>
          <nuxt-link class="text-white hover:text-teal-500 text-lg px-4 py-3" to="#">Features</nuxt-link>
        </li>
        <li>
          <nuxt-link class="text-white hover:text-teal-500 text-lg px-4 py-3" to="#">Success Stories</nuxt-link>
        </li>
      </ul>
      <ul class="flex ml-auto items-center mt-2" v-if="!$store.state.auth.loggedIn">
        <li>
          <nuxt-link to="/register"
            class="inline-block bg-transparent border-white border hover:bg-white hover:bg-opacity-25 text-white font-light w-40 text-center px-6 py-1 text-lg rounded-full mr-4">
            Sign Up
          </nuxt-link>
        </li>
        <li>
          <nuxt-link to="/login"
            class="inline-block bg-transparent border-white border hover:bg-white hover:bg-opacity-25 text-white font-light w-40 text-center px-6 py-1 text-lg rounded-full">
            My Account
          </nuxt-link>
        </li>
      </ul>
      <div class="flex ml-auto" v-else>
        <div class="dropdown inline-block relative z-10">
          <button class="bg-white text-gray-700 font-semibold py-4 px-6 rounded inline-flex items-center">
            <img 
              v-if="$store.state.auth.user.image_url"
              :src="$axios.defaults.baseURL + '/' + $store.state.auth.user.image_url" alt="" class="h-8 rounded-full mr-2">
              <span class="mr-1">
                {{ $store.state.auth.user.name }}
              </span>
          </button>
          <ul class="dropdown-menu absolute hidden text-gray-700 pt-1 shadow w-full">
            <li>
              <nuxt-link to="/dashboard" class="bg-white hover:bg-gray-100 hover:text-orange-500 py-2 px-4 block whitespace-no-wrap">My Dashboard</nuxt-link>
            </li>
            <li>
              <nuxt-link to="/dashboard" class="bg-white hover:bg-gray-100 hover:text-orange-500 py-2 px-4 block whitespace-no-wrap">Account Setting</nuxt-link>
            </li>
            <li>
              <a 
                @click="logout()"
                class="cursor-pointer rounded-b bg-white hover:bg-gray-100 hover:text-orange-500 py-2 px-4 block whitespace-no-wrap">Log out</a>
            </li>
          </ul>
        </div>
      </div>
    </header>
</template>

<script>
export default {
  methods: {
    async logout(){
     this.$auth.logout();
    }
  }
}
</script>

<style scoped>
  .dropdown:hover .dropdown-menu {
    display: block;
  }
</style>