<template>
  <div class="luna-demo">
    <luna-canvas theme="light" />
    <luna-canvas theme="dark" />
  </div>
</template>

<script>
import LunaCanvas from '../components/LunaCanvas.vue';

export default {
  name: 'Demo',
  components: {
    LunaCanvas,
  },
};
</script>

<style>
.luna-demo {
  margin-top: 60px;
  text-align: center;
  background: lightgray;
  padding: 10px;
}
</style>
