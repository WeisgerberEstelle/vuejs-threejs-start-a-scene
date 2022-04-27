<template>
  <div
    @click="onClick()"
    class="tray__swatch"
    :style="{ background: `#${color}`}"
  ></div>
</template>
<script>
export default {
  
  name: "ColorOption",
  props: {
    color: String,
  },
  methods: {
    onClick() {
      this.$emit("color-click");
    },
  },
};
</script>
