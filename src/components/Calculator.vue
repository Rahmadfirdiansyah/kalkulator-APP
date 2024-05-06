<template>
  <body>
    <h1 class="fw-bold">Kalkulator</h1>
    <div
      class="p-3 rounded shadow-box"
      style="max-width: 400px; margin: 50px auto; background: #234"
    >
      <div
        class="w-full rounded m-1 p-3 fw-bold text-end lead text-white bg-vue-dark"
      >
        {{ calculatorValue || 0 }}
      </div>

      <div class="row no-gutters">
        <div class="col-3" v-for="n in calculatorElements" :key="n">
          <div
            class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
            :class="{
              'bg-vue-green': ['C', '*', '/', '-', '+', '%', '='].includes(n),
            }"
            @click="action(n)"
          >
            {{ n }}
          </div>
        </div>
      </div>
    </div>
  </body>
</template>

<script>
export default {
  name: "Calculator",
  props: {
    msg: String,
  },
  data() {
    return {
      calculatorValue: "",
      calculatorElements: [
        "C",
        "*",
        "/",
        "-",
        7,
        8,
        9,
        "+",
        4,
        5,
        6,
        "%",
        1,
        2,
        3,
        "=",
        0,
        ".",
      ],
      operator: null,
      previousCalculatorValue: "",
    };
  },

  methods: {
    action(n) {
      if (!isNaN(n) || n === ".") {
        this.calculatorValue += n + "";
      }
      if (n === "C") {
        this.calculatorValue = "";
      }
      if (n === "%") {
        this.calculatorValue = this.calculatorValue / 100 + "";
      }
      if (["/", "*", "-", "+"].includes(n)) {
        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = "";
      }

      if (n === "=") {
        this.calculatorValue = eval(
          this.previousCalculatorValue + this.operator + this.calculatorValue
        );

        (this.previousCalculatorValue = ""), (this.operator = null);
      }
    },
  },
};
</script>

<style>
body {
  background: linear-gradient(
    90deg,
    hsla(145, 84%, 73%, 1) 0%,
    hsla(150, 61%, 48%, 1) 100%
  );
}

h1{
  justify-content: center;
  display: flex;
  position: relative;
  top: 23px;
}

.shadow-box {
  box-shadow: rgba(0, 0, 0, 0.19) 0px 10px 20px, rgba(0, 0, 0, 0.23) 0px 6px 6px; 
}

.bg-vue-dark {
  background: #31475e;
}

.hover-class {
  cursor: pointer;
}
.hover-class:hover {
  background: #3d5875;
}

.bg-vue-green {
  background: #3fb984;
}
.bg-vue-green:hover {
  background: #257955;
}
</style>
