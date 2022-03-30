<template>
  <div class="bg-dark h-screen overflow-hidden">
    <div class="flex h-[90vh]">
      <!-- Side Bar -->
      <div class="w-60 bg-black h-full flex-none flex flex-col hidden lg:block">
        <div class="p-6 flex items-center justify-center">
          <img
            src="https://radio-app-r4vit3j4.netlify.app/img/test.bac0d12e.png"
            class="invert h-[50px]"
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
            <div
              class="w-full mt-2 h-56 overflow-y-scroll overflow-x-hidden scrl"
            >
              <p
                v-for="album in albums"
                :key="album.name"
                class="text-lightest hover:text-white text-sm py-[6px] whitespace-nowrap line-clamp-1"
              >
                {{ album.name }}
              </p>
            </div>

            <div class="mt-3">
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
              class="p-2 pt-3 w-96 flex-shrink-0 lg:mb-2"
            >
              <div
                class="hover:bg-light cursor-pointer transition-all duration-300 bg-[rgba(40,40,40,0.25)] min-h-[340px] w-full h-auto p-5 pt-4 rounded-lg shadow-md"
                @click="handleClick(item.index)"
              >
                <img :src="item.src" class="h-[190px] w-full shadow mb-2" />
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
      class="w-full sticky bottom-0 border-t border-light bg-[#181818] h-[10vh] min-h-[80px] flex items-center justify-between px-6"
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
        <div class="flex items-center space-x-5">
          <i
            class="ti cursor-pointer ti-player-skip-back text-lightest hover:text-white text-xl"
          ></i>

          <div
            @click="!isPlaying ? playSong(5) : pauseSong(5)"
            class="cursor-pointer"
          >
            <PlayIcon v-if="!isPlaying" class="text-black invert h-10 w-10" />
            <!-- <i
              v-if="!isPlaying"
              class="ti ti-player-play text-black text-xl"
            ></i> -->
            <PauseIcon v-else class="text-black invert h-10 w-10" />
            <!-- <i v-else class="ti ti-player-pause text-black text-xl"></i> -->
          </div>
          <i
            class="ti cursor-pointer ti-player-skip-forward text-lightest hover:text-white text-xl"
          ></i>
        </div>
        <!-- <div class="flex text-xs items-center space-x-2">
          <p>2:10</p>
          <input type="range" class="h-1 lg:w-96 md:w-72 w-40" />
          <p>7:09</p>
        </div> -->
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
          @input="updateVolume"
          class="w-24 h-[3px] hidden md:inline-block"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { PlayIcon, PauseIcon } from "@heroicons/vue/solid";
export default {
  name: "App",
  components: {
    PauseIcon,
    PlayIcon,
  },
  computed: {
    volume_dec() {
      return this.volume / 100;
    },
  },
  methods: {
    handleClick(index) {
      if (this.isPlaying) {
        this.pauseSong(index);
      } else this.playSong(index);
    },
    playSong(index) {
      if (index === 5) {
        this.player = new Audio(
          "https://coderadio-relay-blr.freecodecamp.org/radio/8010/low.mp3"
        );
        this.player.play();
        this.player.volume = 0.5;
        this.isPlaying = true;
      }
    },
    pauseSong(index) {
      this.player.pause();
      delete this.player;
      this.player = null;
      this.isPlaying = false;
    },
    updateVolume() {
      this.player.volume = this.volume_dec;
      console.log(this.volume_dec, this.player.volume);
    },
  },
  data() {
    return {
      player: null,
      showDropDown: false,
      isPlaying: false,
      volume: 50,

      isVolumeShowing: false,
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
          index: 0,
        },
        {
          src: "https://i.ytimg.com/vi/kgx4WGK0oNU/hq720.jpg",
          title:
            "jazz/lofi hip hop radio🌱chill beats to relax/study to [LIVE 24/7]",
          artist: "阿鲍Abao",
          index: 0,
        },
        {
          src: "https://i.ytimg.com/vi/N65Jb683pXQ/hq720.jpg",
          title:
            "Spinnin' | 24/7 Live Radio | Deep House, Chill House | Dance Music to relax/study to",
          artist: "Spinnin Records",
          index: 0,
        },
        {
          src: "https://i.ytimg.com/vi/WDXPJWIgX-o/hqdefault.jpg?sqp=-oaymwEcCOADEI4CSFXyq4qpAw4IARUAAIhCGAFwAcABBg==&rs=AOn4CLD5ppCZ18qs8ii5MF-XJMZNz6YnDA",
          title: "anime lofi hip hop radio - 24/7 chill lofi remixes of anime",
          artist: "Lofi Girl",
          index: 0,
        },
        {
          src: "https://i.ytimg.com/vi/ceqgwo7U28Y/hq720.jpg",
          title: "ＣＨＩＬＬ　ＲＡＤＩＯ ２４／７",
          artist: "the bootleg boy 2",
          index: 0,
        },
        {
          src: "https://cdn-media-1.freecodecamp.org/code-radio/bg.jpg",
          title: "Code Radio 24/7 music designed for coding",
          artist: "FreeCodeCamp",
          index: 5,
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

input[type="range"] {
  height: 16px;
  -webkit-appearance: none;
  background: #181818;
  margin: 10px 0;
  /* width: 100%; */
}
input[type="range"]:focus {
  outline: none;
}
input[type="range"]::-webkit-slider-runnable-track {
  width: 100%;
  height: 3px;
  cursor: pointer;
  box-shadow: 0px 0px 0px #000000;
  background: #1db954;
  border-radius: 50px;
  border: 0px solid #000000;
}
input[type="range"]::-webkit-slider-thumb {
  box-shadow: 0px 0px 0px #000000;
  border: 1px solid #ffffff;
  height: 10px;
  width: 10px;
  border-radius: 25px;
  background: #ffffff;
  cursor: pointer;
  -webkit-appearance: none;
  margin-top: -3.5px;
}
input[type="range"]:focus::-webkit-slider-runnable-track {
  background: #1db954;
}
input[type="range"]::-moz-range-track {
  width: 100%;
  height: 3px;
  cursor: pointer;
  box-shadow: 0px 0px 0px #000000;
  background: #1db954;
  border-radius: 50px;
  border: 0px solid #000000;
}
input[type="range"]::-moz-range-thumb {
  box-shadow: 0px 0px 0px #000000;
  border: 1px solid #ffffff;
  height: 9px;
  width: 9px;
  border-radius: 50px;
  background: #ffffff;
  cursor: pointer;
}
input[type="range"]::-ms-track {
  width: 100%;
  height: 3px;
  cursor: pointer;
  background: transparent;
  border-color: transparent;
  color: transparent;
}
input[type="range"]::-ms-fill-lower {
  background: #1db954;
  border: 0px solid #000000;
  border-radius: 100px;
  box-shadow: 0px 0px 0px #000000;
}
input[type="range"]::-ms-fill-upper {
  background: #1db954;
  border: 0px solid #000000;
  border-radius: 100px;
  box-shadow: 0px 0px 0px #000000;
}
input[type="range"]::-ms-thumb {
  margin-top: 1px;
  box-shadow: 0px 0px 0px #000000;
  border: 1px solid #ffffff;
  height: 9px;
  width: 9px;
  border-radius: 50px;
  background: #ffffff;
  cursor: pointer;
}
input[type="range"]:focus::-ms-fill-lower {
  background: #1db954;
}
input[type="range"]:focus::-ms-fill-upper {
  background: #1db954;
}
</style>
