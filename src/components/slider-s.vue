<template>
  <v-layout>
    <v-card v-for="(preset, index) in presets.state" :key="`preset-${index}`" width="250" outlined :class="'pa-0 ' + 'ma-2 ' ">
        <pwm-preset :datas="presets.state[index]"></pwm-preset>
        <v-btn color="success" @click="sendNew">Send</v-btn>
    </v-card>
  </v-layout>
</template>

<script>
  import PwmPreset from "./pwm-preset.vue";
  import { axios } from '@/plugins/axios';
  var root = window.location.origin;
  var baseURL = root + "/device/config/state/";

export default {
  name: "SliderS",
  components: {
     PwmPreset,
  },

  methods: {
    toggleVisibility: function(){
      this.isVisible = !this.isVisible;
    },
    sendNew: function() {
      axios.post(baseURL, this.presets);
    },
  },
  computed: {

  },

  async mounted() {
    try {
      const res = await axios.get(baseURL)

      this.presets = res.data;
    } catch (e) {
        console.error(e)
      }
    },
  data(){ 
    return {
      isVisible: false,
      presets:[],
    }
  }

};
</script>

<style>

</style>