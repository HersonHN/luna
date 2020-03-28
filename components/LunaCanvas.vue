<template>
  <div
    class="luna-canvas"
    :class="[theme]"
  >
    <canvas
      ref="canvas"
      class="luna"
      :width="sizeX"
      :height="sizeY"
      @click="point"
    />
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
    width: {
      type: Number,
      default: 100,
    },
    height: {
      type: Number,
      default: 100,
    },
    pixelSize: {
      type: Number,
      default: 3,
    },
  },
  data() {
    return {
      canvas: null,
      ctx: null,
      sizeX: 0,
      sizeY: 0,
      fillStyle: 'black',
    };
  },

  watch: {
    theme: function() {
      this.redraw();
    }
  },

  mounted() {
    this.canvas = this.$refs.canvas;
    this.ctx = this.canvas.getContext('2d');
    this.sizeX = this.width * this.pixelSize;
    this.sizeY = this.height * this.pixelSize;
    this.matrix = matrix({ lines: this.height, columns: this.width });
  },

  methods: {
    point(event) {
      const { offsetX, offsetY } = event;
      const col = Math.floor(offsetX / this.pixelSize);
      const row = Math.floor(offsetY / this.pixelSize);

      this.matrix[row][col] = true;
      this.paint({ col, row });
    },

    paint({ col, row }) {
      const canvasX = col * this.pixelSize;
      const canvasY = row * this.pixelSize;

      this.ctx.beginPath();
      this.ctx.fillStyle = this.fillStyle;
      this.ctx.rect(canvasX, canvasY, this.pixelSize, this.pixelSize);
      this.ctx.fill();
    },

    redraw() {
      if (this.theme == 'dark') {
        this.fillStyle = 'white';
      } else {
        this.fillStyle = 'black';
      }

      this.ctx.clearRect(0, 0, this.sizeX, this.sizeY);

      const rows = this.matrix;
      for (let row = 0; row < rows.length; row++) {
        let cols = rows[row];
        for (let col = 0; col < cols.length; col++) {
          if (this.matrix[row][col]) {
            this.paint({ col, row });
          }
        }
      }
    },
  },

};

function matrix({ lines, columns }) {
  const arr = [];

  for (let x = 0; x < lines; x++) {
    arr.push([]);

    for (let y = 0; y < columns; y++) {
      arr[x][y] = false;
    }
  }

  return arr;
}

</script>

<style scoped>
  .luna-canvas {
    display: inline-block;
  }

  .luna-canvas.light { background: white; }
  .luna-canvas.dark { background: black; }

  canvas.luna {
    display: block;
  }
</style>
