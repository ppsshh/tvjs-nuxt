<template>
  <div class="container">
    <trading-vue
      :data="chart"
      :overlays="overlays"
      :extensions="ext"
      :legend-buttons="['display', 'settings', 'up', 'down', 'add', 'remove']"
      :toolbar="true"
      titleTxt="To the moon 📈"
      :width="width"
      :height="height"
    ></trading-vue>
  </div>
</template>

<script>
import { TradingVue, DataCube } from "trading-vue-js";
import Overlays from "tvjs-overlays";
import ChartExtensions from "tvjs-xp";
import Circles from "@/components/Circles";
import dataJson from "@/data.js";

export default {
  name: "app",
  components: { TradingVue, Circles },
  data() {
    return {
      width: window.innerWidth,
      height: window.innerHeight,
      overlays: [...Object.values(Overlays), Circles],
      chart: new DataCube({
        chart: {
          type: "Candles",
          data: dataJson
        },
        onchart: [
          {
            name: "EMA",
            type: "EMA",
            data: [],
            settings: {}
          }
        ],
        offchart: [
          {
            name: "MACD",
            type: "MACD",
            data: [],
            settings: {
              histColors: ["#35a776", "#79e0b3", "#e54150", "#ea969e"]
            }
          }
        ]
      }),
      ext: Object.values(ChartExtensions)
    };
  },
  mounted() {
    window.addEventListener("resize", this.onResize);
    this.onResize();
  },
  methods: {
    onResize(event) {
      this.width = window.innerWidth;
      this.height = window.innerHeight;
    }
  }
};
</script>

<style>
body {
  margin: 0;
  overflow: hidden;
}
</style>
