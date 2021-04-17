<template>
  <v-app>
    <v-navigation-drawer app mini-variant permanent>
    <v-list dense>
      <v-list-item
          v-for="item in items"
          :key="item.title"
          :to="item.link"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-system-bar app >
      <v-spacer></v-spacer>
      <v-icon class="mr-0 ml-1">mdi-water-percent</v-icon><span>{{data.humidity}}%</span>
      <v-icon class="mr-0 ml-1">mdi-thermometer</v-icon><span>{{data.temperature}}&deg;C</span>
      <v-icon class="mr-0 ml-1">mdi-clock-outline</v-icon><span>{{data.time}}</span>
    </v-system-bar>
    <v-main>
      <v-container fluid>
        <router-view></router-view>
      </v-container>
    </v-main>
      <v-footer app>
    <!-- -->
  </v-footer>
  </v-app>
</template>

<script>
  import { axios } from '@/plugins/axios';
  var root = process.env.VUE_APP_URL;
  var baseURL = root + "/device/data/";

export default {
  name: 'App',

  components: {
  },

  data: () => ({
    items: [
          { title: 'Home', icon: 'mdi-view-dashboard', link: '/' },
          { title: 'Network', icon: 'mdi-access-point', link: '/network' },
          { title: 'About', icon: 'mdi-help-box', link: '/about'},
        ],
    data: {
      temperature: 15,
      humidity: 10,
      time: "12:00"
    }
  }),
  mounted: function () {
      this.loadData();

      setInterval(function () {
        this.loadData();
      }.bind(this), 5000);
  },
  methods: {
    async loadData() {
      try {
        const res = await axios.get(baseURL)

        this.data = res.data;
      } catch (e) {
          console.error(e)
        }
      },
  },

};
</script>
