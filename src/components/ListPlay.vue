<template>
    <div>
        <div class="playlist"
          v-on:click="clickSong">
            <div class="song"
              v-for="(s, index) in song"
              :key="index"
              :data-index="index"
              v-on:click="clickSong"
            >
                <div class="thumb" :style="{'background-image': 'url(' + song[index].image +')'}">
                </div>
                <div class="body">
                    <h3 class="title">{{ song[index].name }}</h3>
                    <p class="author">{{ song[index].singer }}</p>
                </div>
                <div class="option">
                    <i class="fas fa-ellipsis-h"></i>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'list-play',
    props: {
      song: {Type: Array, default: []},
      isPlaying: {Type: [Number, String], default: 0},
      playMusic: {Type: Boolean, default: false}
    },
    data(){
      return{
        
      }
    },
    methods: {
      clickSong(e){
        let songNode = e.target.closest('.song:not(.active)');
        let data;
        if(songNode || e.target.closest('.option')){
          if(songNode){
            data = songNode.dataset.index;
          }
        }
        audio.play();
        this.$emit('handleClickSong', data);
      }
    }
}
</script>

<style>

/* PLAYLIST */
.playlist {
  margin-top: 408px;
  padding: 12px;
}

.song {
  display: flex;
  align-items: center;
  margin-bottom: 12px;
  background-color: #fff;
  padding: 8px 16px;
  border-radius: 5px;
  box-shadow: 0 2px 3px rgba(0, 0, 0, 0.1);
}

.song.active {
  background-color: var(--primary-color);
}

.song:active {
  opacity: 0.8;
}

.song.active .option,
.song.active .author,
.song.active .title {
  color: #fff;
}

.song .thumb {
  width: 44px;
  height: 44px;
  border-radius: 50%;
  background-size: cover;
  margin: 0 8px;
}

.song .body {
  flex: 1;
  padding: 0 16px;
}

.song .title {
  font-size: 18px;
  color: var(--text-color);
}

.song .author {
  font-size: 12px;
  color: #999;
}

.song .option {
  padding: 16px 8px;
  color: #999;
  font-size: 18px;
}
</style>