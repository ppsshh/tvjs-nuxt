<template>
  <div class="container">
    <trading-vue
      :data="chart"
      :overlays="overlays"
      :extensions="ext"
      :legend-buttons="['display']"
    ></trading-vue>
  </div>
</template>

<script>
import { TradingVue, DataCube } from "trading-vue-js";
import ChartExtensions from "tvjs-xp";
import EMA from "@/components/EMA";

export default {
  name: "app",
  components: { TradingVue, EMA },
  data() {
    return {
      overlays: [EMA],
      chart: new DataCube({
        chart: {
          type: "Candles",
          data: [
            [1551128400000, 33, 37.1, 14, 14, 196],
            [1551132000000, 13.7, 30, 6.6, 30, 206],
            [1551135600000, 29.9, 33, 21.3, 21.8, 74],
            [1551139200000, 21.7, 25.9, 18, 24, 140],
            [1551142800000, 24.1, 24.1, 24, 24.1, 29]
          ]
        },
        onchart: [
          {
            name: "Setups",
            type: "Setups",
            data: [[1551128400000, 1, 35]],
            settings: {}
          }
        ]
      }),
      ext: Object.values(ChartExtensions)
    };
  }
};
</script>
