<template>
  <div id="app">
    <header class="h-56 flex flex-col items-center">
      <h1 class="pt-6 text-2xl font-medium text-white tracking-wider">
        IP Address Tracker
      </h1>

      <div class="flex justify-center pt-4 md:w-full">
        <input
          type="text"
          class="px-4 py-2 md:w-1/3 border rounded-tl-md rounded-bl-md text-sm text-gray-800 tracking-wider leading-none focus:outline-none focus:shadow-outline focus:bg-gray-100"
          placeholder="Search for any IP address or domain"
          v-model="search"
        />
        <button
          class="inline-block w-10 flex items-center justify-center bg-gray-900 hover:opacity-75 focus:outline-none focus:shadow-outline border-0 rounded-tr-md rounded-br-md"
        >
          <svg xmlns="http://www.w3.org/2000/svg" width="11" height="14">
            <path fill="none" stroke="#FFF" stroke-width="3" d="M2 1l6 6-6 6" />
          </svg>
        </button>
      </div>
    </header>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      search: ''
    };
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Rubik:wght@400;500;700&display=swap');

#app {
  font-family: 'Rubik', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

header {
  background: url('./assets/images/pattern-bg.png');
}
</style>
