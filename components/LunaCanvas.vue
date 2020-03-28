<template>
  <div
    class="luna-canvas"
    :class="[theme]"
  >
    <canvas class="luna" />
  </div>
</template>

<script>
export default {
  name: 'LunaCanvas',
  props: {
    theme: {
      type: String,
      default: 'light',
    },
  },
  data() {
    return {

    };
  },

  created() {
  },
};
</script>

<style scoped>
  .luna-canvas {
    display: inline-block;
  }

  .luna-canvas.light { background: white; }
  .luna-canvas.dark { background: black; }

  canvas.luna {
    display: block;
    width: 300px;
    height: 300px;
  }
</style>
