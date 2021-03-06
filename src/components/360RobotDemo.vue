<template>
  <div>
    <router-view></router-view>
    <div class=''>
      <div id="back-button" @click="goBack()">
        <q-icon name="keyboard_backspace"></q-icon>
      </div>
      <div id='videojs-panorama-player'>
        <div class='player-wrapper'>
          <div class='player-container'>
            <video id="video-custom" class='video-js vjs-sublime-skin' crossOrigin='anonymous' controls loop ref='video'>
            </video>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import videojs from 'video.js'
import {QIcon} from 'quasar'

export default {
  data () {
    return {
      videoInfo: {
        videoURL: './statics/360RobotDemo.mp4'
      }
    }
  },
  methods: {
    initializePlayer () {
      var videoElement = this.$refs.video
      screen.orientation.lock('landscape')

      this.player = videojs(videoElement, {}, () => {
        window.addEventListener('resize', () => {
          var widthResize = window.innerWidth
          var heightResize = window.innerHeight
          this.player.width(widthResize)
          this.player.height(heightResize)
        })
      })
      var width = window.innerWidth
      var height = window.innerHeight
      this.player.width(width)
      this.player.height(height)
      this.player.src({ src: this.videoInfo.videoURL, type: 'video/mp4' })
    },
    goBack () {
      window.history.back()
    }
  },
  mounted () {
    this.initializePlayer()
  },
  destroyed () {
    this.player.dispose()
  },
  components: {
    QIcon
  }
}

</script>

<style lang='scss'>
video,
#video-custom,
.video-js,
.vjs-default-skin {
  position: fixed;
  right: 0;
  bottom: 0;
  min-width: 100%;
  min-height: 100%;
  width: auto;
  height: auto;
}

#back-button {
  position: absolute;
  top: 0;
  left: 5px;
  z-index: 500;
  font-size: 50px;
  color: white;
}

.vjs_video_3-dimensions {
  width: 100%;
}
.video-js {
  font-size: 10px;
  color: #fff;
}
.vjs-sublime-skin .vjs-big-play-button {
  font-size: 8em;
  line-height: 1.5em;
  height: 1.5em;
  width: 3em;
  border: 0;
  border-radius: .3em;
  left: 50%;
  top: 50%;
  margin-left: -1.5em;
  margin-top: -.75em;
}
.video-js .vjs-big-play-button,
.video-js .vjs-control-bar,
.video-js .vjs-menu-button .vjs-menu-content {
  background-color: #2b333f;
  background-color: rgba(43, 51, 63, .7);
  background-color: transparent;
}
.video-js .vjs-slider {
  background-color: #73859f;
  background-color: rgba(115, 133, 159, .5);
  background-color: rgba(255, 255, 255, .3);
  border-radius: 2px;
  height: 6.5px;
}
.video-js .vjs-play-progress,
.video-js .vjs-slider-bar,
.video-js .vjs-volume-level {
  background: #fff;
}
.video-js .vjs-progress-holder .vjs-load-progress,
.video-js .vjs-progress-holder .vjs-load-progress div,
.video-js .vjs-progress-holder .vjs-play-progress,
.video-js .vjs-progress-holder .vjs-tooltip-progress-bar {
  height: 6.5px;
}
.video-js .vjs-load-progress {
  background: ligthen(#73859f, 25%);
  background: rgba(115, 133, 159, .5);
}
.video-js .vjs-load-progress div {
  background: ligthen(#73859f, 50%);
  background: rgba(115, 133, 159, .75);
}
.vjs-sublime-skin .vjs-poster {
  outline: 0;
  outline: 0;
}
.vjs-sublime-skin:hover .vjs-big-play-button {
  background-color: transparent;
}
.vjs-sublime-skin .vjs-fullscreen-control:before,
.vjs-sublime-skin.vjs-fullscreen .vjs-fullscreen-control:before {
  content: '';
}
.vjs-sublime-skin.vjs-fullscreen .vjs-fullscreen-control {
  background: #fff;
}
.vjs-sublime-skin .vjs-fullscreen-control {
  border: 3px solid #fff;
  box-sizing: border-box;
  cursor: pointer;
  margin-top: -7px;
  top: 50%;
  height: 14px;
  width: 22px;
  margin-right: 10px;
}
.vjs-sublime-skin.vjs-fullscreen .vjs-fullscreen-control:after {
  background: #000;
  content: "";
  display: block;
  position: absolute;
  bottom: 0;
  left: 0;
  height: 5px;
  width: 5px;
}
.vjs-sublime-skin .vjs-progress-holder {
  margin: 0;
}
.vjs-sublime-skin .vjs-progress-control .vjs-progress-holder:after {
  border-radius: 2px;
  display: block;
  height: 6.5px;
}
.vjs-sublime-skin .vjs-progress-control .vjs-load-progres,
.vjs-sublime-skin .vjs-progress-control .vjs-play-progress {
  border-radius: 2px;
  height: 6.5px;
}
.vjs-sublime-skin .vjs-playback-rate {
  display: none;
}
.vjs-sublime-skin .vjs-progress-control {
  margin-right: 50px;
}
.vjs-sublime-skin .vjs-time-control {
  right: 55px;
}
.vjs-sublime-skin .vjs-volume-menu-button:before {
  width: 1.2em;
  z-index: 1;
}
.vjs-sublime-skin .vjs-volume-menu-button .vjs-menu,
.vjs-sublime-skin .vjs-volume-menu-button.vjs-slider-active .vjs-menu,
.vjs-sublime-skin .vjs-volume-menu-button:focus .vjs-menu {
  display: block;
  opacity: 1;
}
.vjs-sublime-skin .vjs-volume-menu-button, .vjs-sublime-skin .vjs-volume-panel {
  width: 6em;
  position: absolute;
  right: 0;
  margin-right: 30px;
}
.vjs-sublime-skin .vjs-volume-menu-button .vjs-menu-content,
.vjs-sublime-skin .vjs-volume-menu-button.vjs-slider-active,
.vjs-sublime-skin .vjs-volume-menu-button:focus,
.vjs-sublime-skin .vjs-volume-menu-button:hover,
.vjs-sublime-skin .vjs-volume-panel .vjs-volume-control,
.vjs-sublime-skin .vjs-volume-panel.vjs-slider-active,
.vjs-sublime-skin .vjs-volume-panel:focus,
.vjs-sublime-skin .vjs-volume-panel:hover {
  width: 6em;
}
.vjs-sublime-skin .vjs-volume-menu-button .vjs-menu {
  left: 23px;
}
.vjs-sublime-skin .vjs-mouse-display:before,
.vjs-sublime-skin .vjs-play-progress:before,
.vjs-sublime-skin .vjs-volume-level:before {
  content: '';
}
.vjs-sublime-skin .vjs-mouse-display:after,
.vjs-sublime-skin .vjs-play-progress:after,
.vjs-sublime-skin .vjs-time-tooltip {
  width: 5.5em;
}
.vjs-sublime-skin .vjs-audio-button {
  display: none;
}
.vjs-sublime-skin .vjs-volume-bar {
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACwAAAAcCAQAAACw95UnAAAAMElEQVRIx2NgoBL4n4YKGUYNHkEG4zJg1OCRYDCpBowaPJwMppbLRg0eNXjUYBLEAXWNUA6QNm1lAAAAAElFTkSuQmCC);
  background-size: 22px 14px;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
  max-width: 22px;
  max-height: 14px;
  margin: 7px 4px;
  border-radius: 0;
}
.vjs-sublime-skin .vjs-volume-level {
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACwAAAAcAQAAAAAyhWABAAAAAnRSTlMAAHaTzTgAAAAZSURBVHgBYwAB/g9EUv+JokCqiaT+U4MCAPKPS7WUUOc1AAAAAElFTkSuQmCC);
  background-size: 22px 14px;
  background-repeat: no-repeat;
  max-width: 22px;
  max-height: 14px;
  height: 100%;
}
.vjs-sublime-skin .vjs-volume-panel.vjs-volume-panel-horizontal.vjs-slider-active,
.vjs-sublime-skin .vjs-volume-panel.vjs-volume-panel-horizontal:active,
.vjs-sublime-skin .vjs-volume-panel.vjs-volume-panel-horizontal:focus,
.vjs-sublime-skin .vjs-volume-panel.vjs-volume-panel-horizontal:hover {
  width: 6em;
  transition-property: none;
}
.vjs-sublime-skin .vjs-volume-panel .vjs-mute-control:hover
  ~ .vjs-volume-control.vjs-volume-horizontal {
  width: 3em;
  height: auto;
}
.vjs-sublime-skin .vjs-volume-panel .vjs-mute-control:hover
  ~ .vjs-volume-control {
  transition-property: none;
}
.vjs-sublime-skin .vjs-fullscreen-control .vjs-icon-placeholder {
  display: none;
}
.vjs-sublime-skin .vjs-volume-panel .vjs-mute-control {
  width: 2em;
  z-index: 1;
  padding: 0;
}
.vjs-sublime-skin .vjs-volume-panel .vjs-volume-control {
  display: inline-block;
  position: relative;
  left: 5px;
  opacity: 1;
  width: 3em;
  height: auto;
}
#videojs-panorama-player .vjs-mute-control {
  display: none;
}
#videojs-panorama-player .vjs-fullscreen-control {
  display: none;
}
#videojs-panorama-player .vjs-volume-panel-horizontal {
  display: none;
}
#videojs-panorama-player .vjs-volume-panel {
  display: none;
}
.video-js button {
  font-size: 20px;
}
.video-js .vjs-control-bar {
  height: 4rem;
}
.video-js .vjs-time-control {
  line-height: 4rem;
  right: 30px;
  display: none;
}
#videojs-panorama-player .vjs-VR-control {
  right: 20px;
}
#video-custom > div.vjs-control-bar > div.vjs-volume-menu-button.vjs-menu-button.vjs-menu-button-inline.vjs-control.vjs-button.vjs-volume-menu-button-horizontal.vjs-vol-3 {
  display: none;
}

</style>
