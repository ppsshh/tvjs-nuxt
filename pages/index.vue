<template>
  <div class="container">
    <trading-vue
      :data="chart"
      :overlays="overlays"
      :extensions="ext"
      :legend-buttons="['display', 'settings', 'up', 'down', 'add', 'remove']"
      :night="true"
      :width="1500"
      :height="900"
    ></trading-vue>
  </div>
</template>

<script>
import { TradingVue, DataCube } from "trading-vue-js";
import Overlays from "tvjs-overlays";
import ChartExtensions from "tvjs-xp";
import EMA from "@/components/EMA";
import dataJson from "@/data.js";

export default {
  name: "app",
  components: { TradingVue, EMA },
  data() {
    return {
      overlays: [EMA, Overlays["MACD"]],
      chart: new DataCube({
        chart: {
          type: "Candles",
          data: dataJson
        },
        onchart: [
          {
            name: "EMA",
            type: "Spline",
            data: [
              [1593824400000, 9000, 20],
              [1593828000000, 9000, 35]
            ],
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
  }
};
</script>
