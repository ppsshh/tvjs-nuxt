<script>
import { Overlay } from "trading-vue-js";

export default {
  mixins: [Overlay],
  methods: {
    draw(ctx) {
      for (const p of this.$props.data) {
        var img = document.createElement("img");
        img.src = p[0];
        ctx.drawImage(img);
        console.log("abcdef", p[0]);
      }
    },
    use_for() {
      return ["ExtImage"];
    }
  }
};
</script>
