<template>
  <div class="home">
    <panel></panel>
    <!-- <v-btn
      color="pink"
      dark
      absolute
      top
      right
      fab
    >
      <v-icon>mdi-plus</v-icon>
    </v-btn> -->
  </div>
</template>

<script>
// @ is an alias to /src
// import SliderS from '@/components/slider-s.vue';

import Panel from '@/components/panel.vue';


export default {
  name: 'Home',
  components: {
    Panel
  },
}
</script>
