<template>
  <main>
    <h1>
      PodSinc
      <button @click="toggleVolume">
        <volume-2-icon v-if="!!volume"/>
        <volume-x-icon v-else/>
      </button>
    </h1>
    <p>
      Every 10 seconds a BEEP will chime. Make sure your audio recorder is
      capturing your computer's audio. Be sure not to wear your headphones
      during this time. Click on the volume icon to unmute the beep.
      When you see the word BEEP, you can mute and/or close out of this site.
      Toss your headphones back on and start podcasting! ✌
    </p>
    <h2 v-html="secTimer" />
  </main>
</template>

<script>
import {
  Volume2Icon,
  VolumeXIcon,
} from 'vue-feather-icon-set';
import {
  SECOND,
  getZeroPad,
} from './Filters';
import Beep from '../assets/audio/Beep.mp3';

export default {
  components: {
    Volume2Icon,
    VolumeXIcon,
  },
  data() {
    return {
      seconds: 0,
      beep: null,
      volume: 0,
    };
  },
  created() {
    this.beep = new Audio(Beep);
    this.beep.volume = this.volume;
    this.updateDateTime();
    this.$options.timer = window.setTimeout(this.updateDateTime, SECOND);
  },
  beforeDestroy() {
    window.clearTimeout(this.$options.timer);
  },
  methods: {
    updateDateTime() {
      const now = new Date();
      this.seconds = getZeroPad(now.getSeconds()) % 10;
      this.$options.timer = window.setTimeout(this.updateDateTime, SECOND);
    },
    toggleVolume() {
      if (this.volume === 0) {
        this.volume = 1;
        return this.volume;
      }
      this.volume = 0;
      return this.volume;
    },
  },
  computed: {
    secTimer() {
      if (this.seconds === 0) {
        return 'BEEP';
      }
      return this.seconds;
    },
  },
  watch: {
    seconds() {
      if (this.seconds === 0) {
        this.beep.play();
      }
    },
    volume() {
      this.beep.volume = this.volume;
    },
  },
};
</script>

<style scoped lang="scss">
main {
  display:flex;
  flex-direction: column;
  align-items: center;
  max-width: 400px;
}
h2 {
  font-size: 4rem;
  margin-top: 0;
}
button {
  background-color: transparent;
  color: #35f2ff;
  border:none;
  &:focus {
    outline: none;
  }
}
</style>
