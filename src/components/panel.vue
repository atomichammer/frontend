<template>
<div>
  <v-expansion-panels>
    <v-expansion-panel
      v-for="(preset, index) in presets.state"
      :key="'preset-' + index"
      :class="color1(index) + ' lighten-4'"
    >
      <v-expansion-panel-header class="mb-0">
        <v-layout>
        <v-chip class="mr-2" label outlined @click="lights">
          <v-icon left>
            mdi-clock-outline
          </v-icon>
          {{parseTime(preset.activeFrom)}}
        </v-chip>
        <v-chip class="mr-2" label outlined>
          <v-icon left>
            mdi-flower-outline
          </v-icon>
          {{preset.title}}
        </v-chip>
        </v-layout>
      </v-expansion-panel-header>
      <v-expansion-panel-content>
        <v-switch class="ml-4 mt-0" label="Active" v-model="presets.state[index].active" dense @change="toggleActive(index)"></v-switch>
        <pwm-preset :datas="presets.state[index]" :isVisible="isVisible" @stateChanged="sendNew()"></pwm-preset>
        <v-btn class="ma-1" @click="sendNew()">Update</v-btn>
      </v-expansion-panel-content>
    </v-expansion-panel>
  </v-expansion-panels>
  <v-dialog
      v-model="dialog"
      width="500"
    >
    <v-card>
        <v-card-title class="headline grey lighten-2">
          Privacy Policy
        </v-card-title>

        <v-card-text>
          Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="primary"
            text
            @click="dialog = false"
          >
            I accept
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  <!-- <v-card
    class="mt-4 mx-auto"
    max-width="400"
  >
    <v-sheet
      class="v-sheet--offset mx-auto"
      color="cyan"
      elevation="12"
      max-width="calc(100% - 32px)"
    >
      <v-sparkline
        :value="value"
        color="white"
        line-width="2"
        padding="16"
      ></v-sparkline>
    </v-sheet> -->
  </div>
</template>

<script>

  import PwmPreset from "./pwm-preset.vue";
  import { axios } from '@/plugins/axios';
  var root = process.env.VUE_APP_URL;
  var baseURL =  root + "/device/config/state/";
  console.log(baseURL);

export default {
    name: 'Panel',
    components: {
        PwmPreset,
    },
    async mounted() {
    try {
      const res = await axios.get(baseURL)

      this.presets = res.data;
    } catch (e) {
        console.error(e)
      }
    },
    methods: {
      color1: function(val){
            return this.presets.state[val].active ? 'green' : 'red';
      },
      sendNew: function(val) {
        console.log(val);
        axios.post(baseURL, this.presets);
      },
      toggleActive(val){
        this.presets.state.forEach(function(item, index){
            if(index != val){
                item.active = false;
            }
        }
        )
      },
      lights() {
        alert('LIghts');
      },
      parseTime(minutes){
        return Math.floor(minutes / 60) + ":" + (minutes % 60);
      }
    
    },
    data(){ 
        return {
            isVisible: false,
            presets:[],
            value:[25,26,27,24,23,27],
        }
    }
}
</script>