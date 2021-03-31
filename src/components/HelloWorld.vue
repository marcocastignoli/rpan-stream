<template>
  <div class="container">
    <div class="row">
      <div class="col-12">
        <div class="card">
          <div class="card-body">
            <small>@angry_llama_pants</small>
            <h5 class="card-title">"make a tennis game, like pong"</h5>
            <div class="mt-3">
              <canvas
                ref="pong"
                width="300px"
                height="200px"
                style="background-color: red"
              >
              </canvas>
            </div>
          </div>
        </div>
        <div class="card mt-3">
          <div class="card-body">
            <small>@Jurica1306</small>
            <h5 class="card-title">
              "Make a button that you press and it moves to a random spot on the
              screen and it measures the time between presses, like a clicking
              game"
            </h5>
            <div class="mt-3">
              <button
                class="btn btn-primary"
                :style="{
                  position: buttonPosition,
                  top: buttonTop,
                  left: buttonLeft,
                  zIndex: 1000
                }"
                @click="moveButton"
              >
                Clicked in {{ milliseconds }} ms
              </button>
            </div>
          </div>
        </div>
        <div class="card mt-3">
          <div class="card-body">
            <small>@SkatebrdingsNoSndwch</small>
            <h5 class="card-title">
              "program that will matrix style give me all programming knowledge
              instantly"
            </h5>
            <div class="mt-3">No</div>
          </div>
        </div>
        <div class="card mt-3 mb-3">
          <div class="card-body">
            <small>@donutdoll</small>
            <h5 class="card-title">"Can u make a dancing pug?"</h5>
            <div class="mt-3">
              <img
                src="https://media.tenor.com/images/5b3f09886cd09e1b5b9f2db96b06051f/tenor.gif"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      buttonTop: 0,
      buttonLeft: 0,
      buttonPosition: "relative",
      milliseconds: 0,
      lastDate: Date.now(),
      ctx: null,
      x1: 10,
      y1: 10,
      x2: 280,
      y2: 10,
    };
  },
  props: {
    msg: String,
  },
  methods: {
    moveButton() {
      this.milliseconds = Date.now() - this.lastDate;
      this.lastDate = Date.now();
      this.buttonPosition = "fixed";
      this.buttonTop = `${Math.floor(Math.random() * window.innerHeight)}px`;
      this.buttonLeft = `${
        Math.floor(Math.random() * window.innerWidth) - 150
      }px`;
    },
    getMousePos(canvas, evt) {
      var rect = canvas.getBoundingClientRect();
      return {
        x: evt.clientX - rect.left,
        y: evt.clientY - rect.top,
      };
    },
  },
  mounted() {
    const canvas = this.$refs.pong;
    this.ctx = canvas.getContext("2d");

    const w = 10;
    const h = 50;

    canvas.addEventListener("mousemove", (evt) => {
      const pos = this.getMousePos(canvas, evt);

      this.y1 = pos.y - h / 2;
    });

    setInterval(() => {
      this.ctx.clearRect(0, 0, canvas.width, canvas.height);
      this.ctx.fillRect(this.x1, this.y1, w, h);
      this.ctx.fillRect(this.x2, this.y2, w, h);
    }, 1000 / 60);
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
