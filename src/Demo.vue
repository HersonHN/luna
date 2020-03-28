<template>
  <section class="luna-demo">
    <div class="themes">
      <label>
        <span>Light:</span>
        <input
          v-model="theme"
          type="radio"
          name="theme"
          value="light"
        >
      </label>
      <label>
        <span>Dark:</span>
        <input
          v-model="theme"
          type="radio"
          name="theme"
          value="dark"
        >
      </label>
    </div>

    <luna-canvas
      :theme="theme"
      :pixel-size="15"
      :width="40"
      :height="20"
    />
  </section>
</template>

<script>
import LunaCanvas from '../components/LunaCanvas.vue';

export default {
  name: 'Demo',
  components: {
    LunaCanvas,
  },
  data() {
    return {
      theme: 'light',
    };
  },
};
</script>

<style>
.luna-demo {
  font-family: sans-serif;
  margin-top: 60px;
  text-align: center;
  padding: 1rem;
  background: #eee;
}

.luna-demo .themes {
  margin-bottom: 1rem;
}

.luna-demo label {
  display: block;
}
</style>
