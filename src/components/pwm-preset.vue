<template lang="">
  <div>
    <v-card outlined v-for="(pwm, index) in datas.data" :key="`pwm-${index}`" class="ma-1">
        <v-card-title class="pb-0">{{ pwm.title }}</v-card-title>
        <v-card-text >
            <v-slider v-model="pwm.value" 
                step="1" 
                thumb-label 
                min="0" 
                max="8" 
                :tick-labels="ticksLabels"
                ticks="always"
                :color="pwm.color +  ' lighten-4'"
                :track-color="pwm.color +  ' darken-4'"
            ></v-slider>
            <v-checkbox
            v-model="pwm.throttle"
            label="Throttling"
            class="mb-0 mt-0 pa-0 shrink"
            dense
            ></v-checkbox>
        </v-card-text>
    </v-card>   
  </div>
</template>

<script>

export default {
    name: "PwmPreset",
    props: ['datas'],
    methods: {
        toggleVisible: function() {
           this.isvisible = !this.isvisible;
        },
    },
    data: function() {
        return {
            isVisible: false,
            ticksLabels: ['0','1','2','3','4','5','6','7','8'],
        }
    },
}
</script>

<style>
 .v-checkbox .v-input__control .v-input__slot {
    min-height: auto !important;
    /* display: flex !important; */
  }
</style>