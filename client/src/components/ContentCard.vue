<template>
  <div class="mx-6 grid grid-cols-2 gap-6 md:grid-cols-3 lg:grid-cols-4 mt-10">
    <div
      v-for="game in games"
      :key="game.id"
      class="max-w-md w-full rounded-t-md overflow-hidden bg-[#004445] shadow-lg rounded-xl p-6"
    >
      <div class="flex flex-col">
        <div>
          <div class="relative h-62 w-full mb-3">
            <div class="absolute flex flex-col top-0 right-0 p-3">
              <!-- <button
                class="transition ease-in duration-300 bg-gray-800 hover:text-purple-500 shadow hover:shadow-md text-gray-500 rounded-full w-8 h-8 text-center p-1"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  class="h-6 w-6"
                  viewBox="0 0 20 20"
                  fill="currentColor"
                >
                  <path
                    fill-rule="evenodd"
                    d="M3.172 5.172a4 4 0 015.656 0L10 6.343l1.172-1.171a4 4 0 115.656 5.656L10 17.657l-6.828-6.829a4 4 0 010-5.656z"
                    clip-rule="evenodd"
                  />
                </svg>
              </button> -->
              <button
              v-if="isLogin"
              @click.prevent="addToWishlist(game.id)"
                class="transition ease-in duration-300 bg-gray-800 hover:text-purple-500 shadow hover:shadow-md text-gray-500 rounded-full w-8 h-8 text-center p-1"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  class="h-6 w-6"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke="currentColor"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"
                  />
                </svg>
              </button>
            </div>
            <img
              :src="game.background_image"
              class="object-cover h-48 w-96 rounded-2xl"
            />
          </div>
          <div class="flex-auto justify-evenly">
            <div class="flex flex-wrap">
              <div
                class="w-full flex-none text-sm flex items-center text-gray-600"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  class="h-4 w-4 text-red-500 mr-1"
                  viewBox="0 0 20 20"
                  fill="currentColor"
                >
                  <path
                    d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"
                  />
                </svg>
                <span class="text-gray-400 whitespace-nowrap mr-3">{{
                  game.rating
                }}</span>
              </div>
              <div class="flex items-center w-full justify-between min-w-0">
                <h2
                  class="text-lg mr-auto cursor-pointer text-gray-200 hover:text-purple-500 truncate"
                >
                  {{ game.name }}
                </h2>
              </div>
            </div>

            <div
              class="flex pt-4 space-x-2 text-sm font-medium justify-start"
              @click="gameDetail(game.id)"
            >
              <button
                class="transition ease-in duration-300 inline-flex items-center text-sm font-medium mb-2 md:mb-0 bg-purple-500 px-5 py-2 hover:shadow-lg tracking-wider text-white rounded-full hover:bg-purple-600"
              >
                <span>See Details</span>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div></div>
  </div>
</template>

<script>
export default {
  props: [`games`],
  methods: {
    async gameDetail(data) {
      try {
        // console.log(data);
        this.$store.dispatch(`buyTheGame`, data);
        this.$store.dispatch("getDataGame", data);
        this.$router.push(`/game-detail`);
      } catch (err) {
        console.log(err);
      }
    },
    async addToWishlist(data) {
      try {
        // console.log(data);
        this.$store.dispatch(`addToWishlist`, data);
        this.$store.dispatch("showWishlist", data);
        this.$router.push(`/wishlist`);
      } catch (err) {
        console.log(err);
      }
    },
  },
  computed: {
    isLogin() {
      if(localStorage.getItem(`access_token`)){
        return true
      } else {
        return false
      }
    },
  },
};
</script>
