<template>
  <div class="home">
    <network-s :enabled="true"></network-s>
  </div>
</template>

<script>
// @ is an alias to /src
import NetworkS from '../components/network_s'

export default {
  name: 'Network',
  components: {
    NetworkS
  }
}
</script>
