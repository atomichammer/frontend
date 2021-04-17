<template lang="">
    <div v-if="enabled">
        <v-card width="250">
            <v-card-title>Network Settings</v-card-title>
            <v-card-subtitle>Set your network here</v-card-subtitle>
            <v-card-text>
                <v-form
                ref="form"
                v-model="valid"
                lazy-validation
                >
                <v-text-field
                v-model="settings.ip"
                :counter="15"
                label="IP"
                required
                :readonly="settings.dhcp_enabled"
                ></v-text-field>
                <v-text-field
                v-model="settings.netmask"
                :counter="15"
                label="Network Mask"
                required
                :readonly="settings.dhcp_enabled"
                ></v-text-field>
                <v-text-field
                v-model="settings.gateway"
                :counter="15"
                label="Gateway"
                required
                :readonly="settings.dhcp_enabled"
                ></v-text-field>
                <v-checkbox
                v-model="settings.dhcp_enabled"
                label="DHCP Enabled"
                required
                ></v-checkbox>
                <v-checkbox
                v-model="wifi_enabled"
                label="Wi-Fi Enabled"
                required
                ></v-checkbox>
                    <v-text-field
                v-model="settings.wifi_ssid"
                :counter="10"
                label="Wi-Fi SSID"
                required
                ></v-text-field>
                    <v-text-field
                v-model="settings.wifi_pass"
                :counter="10"
                label="Wi-Fi Password"
                required
                ></v-text-field>
                <v-btn class="ma-1" @click="sendNew()">Update</v-btn>
                </v-form>
            </v-card-text>
        </v-card>
    </div>
</template>

<script>
import { axios } from '@/plugins/axios';
var root = process.env.VUE_APP_URL;
var baseURL = root + "/device/config/network/";
console.log(root);

export default {
  name: "network-s",
  props: {
      enabled: {},
  },
  
  mounted: function () {
    // var user = "admin";
    // var pass = "admin";

    // var authorizationBasic = window.btoa(user + ":" + pass);
    var config = {
      // "headers": {
      //     "Authorization": "Basic " + authorizationBasic,
      // },
      crossdomain: true,
    };
    axios.get(baseURL, config).then((response) => {this.settings = response.data;
                                               this.loading = false});
  },
  methods: {
        sendNew: function() {
            axios.post(baseURL, this.settings);
    },
  },
  
  data: function () {
    return { 
            settings: null, 
            enabled1 : true,
            loading: true,
        };
  },
};
</script>
<style lang="">

</style>