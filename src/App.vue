<template>
  <div class="player"
    v-bind:class="{
      playing: playMusic
    }"
  >
    <!-- Dashboard -->
    <div class="dashboard">
      <!-- Header -->
      <HeaderCD
        v-bind:song="song"
        v-bind:isPlaying="isPlaying"
        v-bind:playMusic="playMusic"
      />

      <!-- Control -->
      <control
        v-bind:song="song"
        v-bind:isPlaying="isPlaying"
        v-bind:playMusic="playMusic"
        v-bind:isRandom="isRandom"
        v-bind:isRepeat="isRepeat"
        v-on:handlePlaying="handlePlaying"
        v-on:handlePlayNextSong="handlePlayNextSong"
        v-on:handlePlayPrevSong="handlePlayPrevSong"
        v-on:handleRandomSong="handleRandomSong"
        v-on:handleNextEnd="handleNextEnd"
        v-on:handleRepeat="handleRepeat"
        v-on:randomSong="randomSong"
      />
    </div>

    <!-- Playlist -->
    <list-play
      v-bind:song="song"
      v-bind:isPlaying="isPlaying"
      v-bind:playMusic="playMusic"
      v-on:handleClickSong="handleClickSong"
    />
  </div>
</template>

<script>
import HeaderCD from './components/HeaderCD.vue';
import Control from './components/Control.vue';
import ListPlay from './components/ListPlay.vue';
export default {
  name: 'app',
  data() {
    return {
      song: [
      {
        "id": 1,
        "name": "Không yêu xin đừng nói",
        "singer": "UMIE",
        "path": "/public/assets/khong_yeu_xin_dung_noi.mp3",
        "image":
          "https://is1-ssl.mzstatic.com/image/thumb/Music116/v4/5f/02/1e/5f021e14-8d8e-6d7d-ad82-b1252fafe5cd/190296376160.jpg/1200x1200bf-60.jpg"
      },
      {
          "id": 2,
        "name": "Until I Found You",
        "singer": "Stephen Sanchez",
        "path":
          "/public/assets/until_i_found_you.mp3",
        "image": "https://upload.wikimedia.org/wikipedia/en/f/f5/Stephen_Sanchez_-_Until_I_Found_You.png"
      },
      {
          "id": 3,
        "name": "Dynasty",
        "singer": "MIIA",
        "path": "/public/assets/dynasty.mp3",
        "image":
          "https://yt3.googleusercontent.com/ytc/AOPolaRb2_yPgvnQsJD8m1jr0eXHLT7F4YXAyRGlx98G=s900-c-k-c0x00ffffff-no-rj"
      },
      {
          "id": 4,
        "name": "Happier",
        "singer": "Raftaar",
        "path": "/public/assets/happier.mp3",
        "image":
          "https://upload.wikimedia.org/wikipedia/en/e/e5/Marshmello_and_Bastille_Happier.png"
      },
      {
          "id": 5,
        "name": "Chắc anh đang",
        "singer": "Tiên Tiên x Trang",
        "path": "/public/assets/chac_anh_dang.mp3",
        "image":
          "https://c-cl.cdn.smule.com/rs-s80/arr/2d/eb/719babb5-408f-43ac-a870-0ad3a06f6ba2.jpg"
      }
      ],
      isPlaying: 0,
      playMusic: false,
      isRandom: false,
      isRepeat: false
    }
  },
  methods: {
    handlePlaying(){
      if(!this.playMusic){
          audio.play();
          this.playMusic = !this.playMusic;
        }
        else{
          audio.pause();
          this.playMusic = !this.playMusic;
        }
      },
      nextSong(){
        this.isPlaying++;
        if(this.isPlaying >= this.song.length)
          this.isPlaying = 0;
      },
      handlePlayNextSong(){
        this.nextSong();
        this.playMusic = true;
      },
      prevSong(){
        this.isPlaying--;
        if(this.isPlaying < 0)
          this.isPlaying = this.song.length-1;
      },
      handlePlayPrevSong(){
        this.prevSong();
        this.playMusic = true;
      },
      randomSong(){
        var newSong
        do{
          newSong =  Math.floor(Math.random() * this.song.length);
        } while (newSong === this.isPlaying)
        this.isPlaying = newSong;
      },
      handleRandomSong(){
        this.isRandom = !this.isRandom;
        this.randomSong();
        this.playMusic = true;
        this.isRepeat = false;
      },
      handleNextEnd(){
        this.nextSong();
      },
      handleRepeat(){
        this.isRepeat = !this.isRepeat;
        this.isRandom = false;
      },
      handleClickSong(data){
        this.isPlaying = data;
        this.playMusic = true;
      }
  },
  components: {
    HeaderCD,
    Control,
    ListPlay
  },
  computed: {
    
  }
}
</script>

<style>
:root {
  --primary-color: #ec1f55;
  --text-color: #333;
}

* {
  padding: 0;
  margin: 0;
  box-sizing: inherit;
}

body {
  background-color: #f5f5f5;
}

html {
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}

.player {
  position: relative;
  max-width: 480px;
  margin: 0 auto;
}

.player .icon-pause {
  display: none;
}

.player.playing .icon-pause {
  display: inline-block;
}

.player.playing .icon-play {
  display: none;
}

.dashboard {
  padding: 16px 16px 14px;
  background-color: #fff;
  position: fixed;
  top: 0;
  width: 100%;
  max-width: 480px;
  border-bottom: 1px solid #ebebeb;
}



</style>
