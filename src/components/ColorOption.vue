<template>
  <div
    @click="$emit('color-click', $event);"
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
};
</script>
