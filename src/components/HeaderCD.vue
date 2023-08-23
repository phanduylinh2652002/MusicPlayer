<template>
    <div class="header-cd">
      <!-- Header -->
        <header>
            <h4>Now playing:</h4>
            <h2>{{ this.song[this.isPlaying].name }}</h2>
        </header>

      <!-- CD -->
      <div class="cd">
        <div class="cd-thumb" 
          :style="{'background-image': 'url(' + this.song[this.isPlaying].image +')'}">
        </div>
      </div>
    </div>
</template>

<script>
export default {
    name: 'header-cd',
    data(){
      return {
        
      }
    },
    props: {
      song: {Type: Array, default:[]},
      isPlaying: {Type: Number, Default: 0}
    },
    methods:{
      
    }
}
</script>
<style>
/* HEADER */
header {
  text-align: center;
  margin-bottom: 10px;
}

header h4 {
  color: var(--primary-color);
  font-size: 12px;
}

header h2 {
  color: var(--text-color);
  font-size: 20px;
}

/* CD */
.cd {
  display: flex;
  margin: auto;
  width: 200px;
}

.cd-thumb {
  width: 100%;
  padding-top: 100%;
  border-radius: 50%;
  background-color: #333;
  background-size: cover;
  margin: auto;
}
</style>