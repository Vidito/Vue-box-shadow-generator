<template>
  <main>
    <h1>Box Shadow Generator</h1>
    <div class="wrapper">
      <div class="left">
        <label for="h-shadow">Horizontal Shadow Length:</label>
        <br />
        <input
          type="range"
          id="h-shadow"
          v-model="hShadow"
          min="-50"
          max="50"
          step="1"
        />
        {{ hShadow }} px<br />
        <hr />

        <label for="v-shadow">Vertical Shadow Length:</label><br />
        <input
          type="range"
          id="v-shadow"
          v-model="vShadow"
          min="-50"
          max="50"
          step="1"
        />
        {{ vShadow }} px<br />
        <hr />

        <label for="blur-radius">Blur Radius:</label><br />
        <input
          type="range"
          id="blur-radius"
          v-model="blurRadius"
          min="0"
          max="50"
          step="1"
        />
        {{ blurRadius }} px<br />
        <hr />

        <label for="spread-radius">Spread Radius:</label><br />
        <input
          type="range"
          id="spread-radius"
          v-model="spreadRadius"
          min="-50"
          max="50"
          step="1"
        />
        {{ spreadRadius }} px<br />
        <hr />

        <label for="container-color">Container Color:</label><br />
        <input
          type="color"
          id="container-color"
          v-model="containerColor"
        /><br />
        <hr />
        <label for="box-color">Box Color:</label><br />
        <input type="color" id="box-color" v-model="boxColor" /><br />
        <hr />
        <label for="shadow-color">Shadow Color:</label><br />
        <input type="color" id="shadow-color" v-model="shadowColor" /><br />
        <hr />

        <label for="opacity">Shadow Color Opacity:</label><br />
        <input
          type="range"
          id="opacity"
          v-model="opacity"
          min="0"
          max="1"
          step="0.1"
        />
        {{ opacity }}<br />
        <hr />

        <pre>box-shadow: {{ boxShadow }}</pre>
        <hr />
        <button class="copyBtn" @click.prevent="copy">Copy CSS Code</button>
      </div>
      <div class="container" :style="{ backgroundColor: containerColor }">
        <div
          class="box"
          :style="{ boxShadow: boxShadow, backgroundColor: boxColor }"
        ></div>
      </div>
    </div>
  </main>
</template>
<script>
export default {
  data() {
    return {
      hShadow: 0,
      vShadow: 0,
      blurRadius: 0,
      spreadRadius: 0,
      containerColor: "#6760c3",
      boxColor: "#fefefe",
      shadowColor: "#000000",
      opacity: 1,
    };
  },
  computed: {
    boxShadow() {
      return `${this.hShadow}px ${this.vShadow}px ${this.blurRadius}px ${
        this.spreadRadius
      }px rgba(${parseInt(this.shadowColor.slice(1, 3), 16)}, ${parseInt(
        this.shadowColor.slice(3, 5),
        16
      )}, ${parseInt(this.shadowColor.slice(5, 7), 16)}, ${this.opacity})`;
    },
  },
  methods: {
    async copy() {
      let shadow = `box-shadow:${this.boxShadow};`;
      await navigator.clipboard.writeText(shadow);

      alert("CSS copied to clipboard!");
    },
  },
};
</script>
<style scoped>
main {
  padding-top: 3rem;
  font-family: "Poppins", sans-serif;
  color: #6760c3;
}
main h1 {
  text-align: center;
}
.wrapper {
  max-width: 900px;
  padding: 2rem;
  display: flex;
  justify-content: space-around;
  align-items: center;
  gap: 5rem;
  margin: 3rem auto;
  background: rgba(255, 255, 255, 0.25);
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
  backdrop-filter: blur(4.5px);
  -webkit-backdrop-filter: blur(4.5px);
  border-radius: 10px;
}

.container {
  padding: 2rem;
  width: 100%;
  height: 100%;
}
.box {
  margin: 4rem auto;
  width: 200px;
  height: 200px;
}
.left {
  line-height: 1.2;
}
.copyBtn {
  padding: 0.5rem 1rem;
  cursor: pointer;
  border: none;
  background: rgba(255, 255, 255, 0.25);
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
  backdrop-filter: blur(4.5px);
  -webkit-backdrop-filter: blur(4.5px);
  border-radius: 10px;
}
@media only screen and (max-width: 700px) {
  .wrapper {
    flex-direction: column;
  }
}
</style>