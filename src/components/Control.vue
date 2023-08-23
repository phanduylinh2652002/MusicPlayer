<template>
    <div>
        <div class="control">
            <div class="btn btn-repeat"
              :class="{active: isRepeat}"
              v-on:click="rePlaySong"
            >
                <i class="fas fa-redo"></i>
            </div>
            <div class="btn btn-prev"
              v-on:click="prevSong"
            >
                <i class="fas fa-step-backward"></i>
            </div>
            <div class="btn btn-toggle-play" 
              v-on:click="playing">
                <i class="fas fa-pause icon-pause"></i>
                <i class="fas fa-play icon-play"></i>
            </div>
            <div class="btn btn-next"
              v-on:click="playNextSong"
            >
                <i class="fas fa-step-forward"></i>
            </div>
            <div class="btn btn-random"
             v-bind:class="{active: isRandom}"
             v-on:click="handleRandomSong"
            >
                <i class="fas fa-random"></i>
            </div>
        </div>

        <input 
          @change="handleChangeTime"
        id="progress" class="progress" type="range" value="0" step="1" min="0" max="100">

        <audio
          @timeupdate="handleRangeTime"
          @ended="whenEnd"
          ref="audioPlay"
          preload="none"
        id="audio" :src="this.song[this.isPlaying].path"></audio>
    </div>
</template>

<script>
export default {
    name: 'control',
    props: {
      song: {Type: Array, default: []},
      isPlaying: {Type: Number, default: 0},
      playMusic: {Type: Boolean, default: false},
      isRandom: {Type: Boolean, default: false},
      isRepeat: {Type: Boolean, default: false}
    },
    data(){
        return{
          
        }
    },
    methods: {
      playing(){
        this.$emit('handlePlaying');
      },
      handleRangeTime(){
        var progress = document.querySelector('#progress');
        if(audio.duration){
           const progressPercent = Math.floor(audio.currentTime / audio.duration * 100);
           progress.value = progressPercent;
        }
      },
      handleChangeTime(e){
        const seekTime = audio.duration / 100 * e.target.value;
        audio.currentTime = seekTime;
      },
      handlePromisePlay(){
        const playAudio = this.$refs.audioPlay.play();
        if(playAudio !== undefined){
          playAudio.then(_=> {
            audio.currentTime = 0;
            audio.play();
          })
          .catch(error => {
            audio.currentTime = 0;
            audio.play();
          });
        }
      },
      playNextSong(){
        this.$emit('handlePlayNextSong');
        this.handlePromisePlay();
      },
      prevSong(){
        this.$emit('handlePlayPrevSong');
        this.handlePromisePlay();
      },
      rePlaySong(){
        this.$emit('handleRepeat');
      },
      handleRandomSong(){
        this.$emit('handleRandomSong');
        this.handlePromisePlay();
      },
      whenEnd(){
        if(!this.isRepeat && !this.isRandom){
          this.$emit('handleNextEnd');
          this.handlePromisePlay();
        }
        if(this.isRepeat){
          this.handlePromisePlay();
        }
        if(this.isRandom){
          this.$emit('randomSong');
          this.handlePromisePlay();
        }
      }
    }
}
</script>

<style>

/* CONTROL */
.control {
  display: flex;
  align-items: center;
  justify-content: space-around;
  padding: 18px 0 8px 0;
}

.control .btn {
  color: #666;
  padding: 18px;
  font-size: 18px;
}

.control .btn.active {
  color: var(--primary-color);
}

.control .btn-toggle-play {
  width: 56px;
  height: 56px;
  border-radius: 50%;
  font-size: 24px;
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: var(--primary-color);
}

.progress {
  width: 100%;
  -webkit-appearance: none;
  height: 6px;
  background: #d3d3d3;
  outline: none;
  opacity: 0.7;
  -webkit-transition: 0.2s;
  transition: opacity 0.2s;
}

.progress::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 12px;
  height: 6px;
  background-color: var(--primary-color);
  cursor: pointer;
}

</style>