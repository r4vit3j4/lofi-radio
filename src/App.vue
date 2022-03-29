<template>
  <div class="bg-dark h-screen">
    <div class="flex h-[88vh]">
      <!-- Side Bar -->
      <div class="w-60 bg-black h-full flex-none flex flex-col hidden lg:block">
        <div class="p-6">
          <img
            src="https://radio-app-r4vit3j4.netlify.app/img/test.bac0d12e.png"
            class="invert h-12"
          />
          <!-- ./assets/logo/spotify-black.png -->
        </div>
        <div class="mx-3 mb-8">
          <button
            v-for="page in pages"
            :key="page.id"
            :class="`w-full text-sm focus:outline-none font-semibold rounded px-3 py-2 flex items-center justify-start ${
              setId === page.id ? 'bg-light text-white' : 'text-lightest'
            }`"
            @click="setId = page.id"
          >
            <img class="invert mr-4" :src="'./src/assets/icons/' + page.icon" />
            <p class="">{{ page.name }}</p>
          </button>
        </div>
        <div class="mx-6 space-y-4">
          <button
            class="flex items-center justify-start opacity-75 hover:opacity-100"
          >
            <div class="bg-white h-6 w-6 items-center justify-center flex mr-4">
              <img class="h-3 w-3" src="./assets/icons/plus.png" />
            </div>
            <p class="text-sm text-white font-semibold">Create Playlist</p>
          </button>
          <button class="flex justify-start opacity-75 hover:opacity-100">
            <!--  -->
            <div class="h-6 w-6 flex items-center justify-center gradient mr-4">
              <img class="h-3 w-3 invert" src="./assets/icons/liked.png" />
            </div>
            <p class="text-sm text-white font-semibold mt-[2px]">Liked Songs</p>
          </button>
          <!-- Divider -->
          <div class="h-px w-full bg-light drop-shadow-md"></div>
        </div>
        <div class="flex-1">
          <div class="ml-6 h-full flex flex-col justify-between">
            <div class="w-full mt-2 h-64 overflow-y-scroll scrl">
              <p
                v-for="album in albums"
                :key="album.name"
                class="text-lightest hover:text-white text-sm py-[6px] whitespace-nowrap"
              >
                {{ album.name }}
              </p>
            </div>

            <div class="mb-3">
              <button
                class="flex items-center justify-start text-white opacity-75 hover:opacity-100"
              >
                <img
                  class="invert h-5 w-5 mr-5"
                  src="./assets/icons/download.png"
                />
                <p class="text-sm font-semibold">Install App</p>
              </button>
            </div>
          </div>
        </div>
      </div>
      <!-- Main Content -->
      <div class="w-full h-full relative overflow-y-scroll scrl">
        <!-- Header -->
        <div
          class="w-full top-0 sticky flex items-center justify-between py-4 px-6 md:px-9 z-20 bg-black/95"
        >
          <div class="flex items-center">
            <button
              class="rounded-full flex items-center justify-center bg-black w-8 h-8 text-white mr-3"
            >
              <i class="ti ti-chevron-left mr-[2px] mb-[2px] text-2xl"></i>
            </button>
            <button
              class="rounded-full flex items-center justify-center bg-black w-8 h-8 text-white"
            >
              <i class="ti ti-chevron-right ml-[2px] mb-[2px] text-2xl"></i>
            </button>
          </div>
          <!-- Dropdown -->
          <div class="relative">
            <button
              @click="showDropDown = !showDropDown"
              class="bg-light hover:bg-[rgba(40,40,40,0.85)] rounded-full py-1 px-1 flex items-center"
            >
              <img
                src="https://avatars.githubusercontent.com/u/75667275?v=4"
                class="h-6 w-6 rounded-full mr-3"
              />
              <p class="text-white font-semibold text-sm mr-3">Ravi Teja</p>
              <i
                v-if="showDropDown === false"
                class="ti ti-caret-down text-white mr-2"
              ></i>
              <i v-else class="ti ti-caret-up text-white mr-2"></i>
            </button>
            <div
              v-if="showDropDown"
              class="absolute bg-light w-full rounded mt-1"
            >
              <button
                class="py-2 text-sm w-full text-lightest hover:text-white border-b border-white opacity-75 hover:opacity-100"
              >
                Account
              </button>
              <button
                class="py-2 text-sm w-full text-lightest hover:text-white border-b border-light opacity-75 hover:opacity-100"
              >
                Logout
              </button>
            </div>
          </div>
        </div>
        <!-- Main body cards -->
        <div class="px-6 md:px-9 py-6">
          <div class="flex items-center justify-between">
            <h1
              class="text-2xl font-semibold tracking-tight text-white hover:underline"
            >
              Lofi Radio's
            </h1>
            <!-- <h2
              class="text-xs pt-4 mb-3 font-bold text-lightest uppercase tracking-wider hover:underline"
            >
              See All
            </h2> -->
          </div>
          <div class="w-full flex flex-wrap justify-center lg:justify-start">
            <div
              v-for="item in BestChart"
              :key="item.title"
              class="p-2 pt-3 cursor-pointer w-96 flex-shrink-0 lg:mb-2"
            >
              <div
                class="hover:bg-light bg-[rgba(40,40,40,0.25)] min-h-[340px] w-full h-auto p-5 pt-4 rounded-lg shadow-md"
              >
                <img :src="item.src" class="h-auto w-full shadow mb-2" />
                <h1
                  class="text-base font-semibold text-white mt-4 my-3 line-clamp-2"
                >
                  {{ item.title }}
                </h1>
                <h2 class="text-xs text-lightest tracking-wide pb-5">
                  {{ item.artist }}
                </h2>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Play bar -->
    <div
      class="w-full sticky bottom-0 border-t border-light bg-[#181818] h-[12vh] min-h-[100px] flex items-center justify-between px-6"
    >
      <!-- Song Info -->
      <div class="flex items-center flex-shrink-0">
        <div class="mr-3">
          <img
            class="h-10 w-10 md:h-14 md:w-14"
            src="https://i.scdn.co/image/ab67616d000048518ac778cc7d88779f74d33311"
          />
        </div>
        <div class="hidden md:block">
          <h1 class="text-sm text-white">Around The World</h1>
          <h2 class="text-xs text-lightest">Daft Punk</h2>
        </div>
      </div>
      <!-- Player -->
      <div class="text-lightest flex flex-col items-center">
        <div class="flex item-center space-x-5 mb-3">
          <i
            class="ti ti-player-skip-back text-lightest hover:text-white text-xl"
          ></i>
          <div class="bg-white rounded-full px-[5px]">
            <i class="ti ti-player-play text-black text-xl"></i>
          </div>
          <i
            class="ti ti-player-skip-forward text-lightest hover:text-white text-xl"
          ></i>
        </div>
        <div class="flex text-xs items-center space-x-2">
          <p>2:10</p>
          <input type="range" class="h-1 lg:w-96 md:w-72 w-40" />
          <p>7:09</p>
        </div>
      </div>
      <!-- Volume -->
      <div class="flex items-center">
        <div class="mr-2">
          <i v-if="volume >= 90" class="ti ti-volume text-lg text-lightest"></i>
          <i
            v-if="volume > 0 && volume < 90"
            class="ti ti-volume-2 text-lg text-lightest"
          ></i>
          <i
            v-if="volume == 0"
            class="ti ti-volume-3 text-lg text-lightest"
          ></i>
        </div>

        <input
          v-model="volume"
          type="range"
          class="w-24 h-[3px] hidden md:inline-block"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      showDropDown: false,
      volume: 50,
      pages: [
        {
          id: "home",
          name: "Home",
          icon: "home.png",
        },
        {
          id: "search",
          name: "Search",
          icon: "search.png",
        },
        {
          id: "library",
          name: "Your Library",
          icon: "library.png",
        },
      ],
      setId: "home",
      albums: [
        {
          name: "My Playlist #4",
        },
        {
          name: "Mellow Lofi 💗 melodic lo-fi",
        },
        {
          name: "The Daily Dose | Indie Bedroom",
        },
        {
          name: "Audio Library -- Chill",
        },
        {
          name: "My Playlist #3",
        },
        {
          name: "My Playlist #4",
        },
        {
          name: "Mello Lofi",
        },
        {
          name: "The Daily Dose | Indie Bedroom",
        },
        {
          name: "Audio Library -- Chill",
        },
        {
          name: "Audio Library -- Chill",
        },
        {
          name: "Audio Library -- Chill",
        },
      ],
      BestChart: [
        {
          src: "https://i.ytimg.com/vi/5qap5aO4i9A/hq720.jpg",
          title: "lofi hip hop radio - beats to relax/study to",
          artist: "Lofi Girl",
        },
        {
          src: "https://i.ytimg.com/vi/kgx4WGK0oNU/hq720.jpg",
          title:
            "jazz/lofi hip hop radio🌱chill beats to relax/study to [LIVE 24/7]",
          artist: "阿鲍Abao",
        },
        {
          src: "https://i.ytimg.com/vi/N65Jb683pXQ/hq720.jpg",
          title:
            "Spinnin' | 24/7 Live Radio | Deep House, Chill House | Dance Music to relax/study to",
          artist: "Spinnin Records",
        },
        {
          src: "https://i.ytimg.com/vi/5qap5aO4i9A/hq720.jpg",
          title: "lofi hip hop radio - beats to relax/study to",
          artist: "Lofi Girl",
        },
        {
          src: "https://i.ytimg.com/vi/5qap5aO4i9A/hq720.jpg",
          title: "lofi hip hop radio - beats to relax/study to",
          artist: "Lofi Girl",
        },
      ],
    };
  },
};
</script>

<style scoped>
.gradient {
  background-image: linear-gradient(
    135deg,
    rgb(69, 10, 245),
    rgb(196, 239, 217)
  );
}
/* .scrl {
  scrollbar-width: thin;
  scrollbar-color: #808080 black;
} */
.scrl::-webkit-scrollbar {
  width: 0.8vw;
}
.scrl::-webkit-scrollbar-thumb {
  background-color: rgb(128, 128, 128, 0.6);
}
</style>
