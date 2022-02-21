<template>
  <div>
    <h1 class="m-5 text-gray-800 text-lg font-bold text-center">
      Simulated live streaming
    </h1>
    <video
      id="video-player"
      controls
      muted
      class="cld-video-player cld-fluid vjs-live cld-video-player-skin-dark w-2/3 h-96 mx-auto" 
    />
    <p class="m-5 text-gray-800 text-sm text-center">
      Video by Taryn Elliott from Pexels
    </p>
  </div>
</template>

<script>
export default {
  data(){
    return {
      cld:null,
      video:'nuxtjs-simulated-live-streaming/video'
    };
  },

  mounted(){
    this.cld = cloudinary.Cloudinary.new({ cloud_name: process.env.NUXT_ENV_CLOUDINARY_CLOUD_NAME });
    let demoplayer = this.cld.videoPlayer(
        'video-player',
        {
          autoplay:true,
          loop: true
        }
      )
      .width(600);
    demoplayer.source(this.video);

    var liveControls = document.getElementsByClassName("vjs-live-control");

    demoplayer.on("play", function () {
      liveControls[0].classList.remove("vjs-hidden");
      
      demoplayer.currentTime(
        parseInt((new Date).getSeconds() % demoplayer.duration())
      ); 
    });
  },
  
}
</script>

<style>

body {
  font-family: sans-serif;
}
.cld-video-player .vjs-control-bar .vjs-progress-control {
  display: none;
}
div.vjs-control-bar > div.vjs-live-control.vjs-control {
  display: block;
}

</style>