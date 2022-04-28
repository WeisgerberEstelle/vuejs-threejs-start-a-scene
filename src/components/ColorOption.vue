<template>
  <div
    v-if="color.texture"
    @click="$emit('color-click', $event)"
    class="tray__swatch"
    :style="{ background: `url(${color.texture})` }"
  ></div>
  <div
    v-else
    @click="$emit('color-click', $event)"
    class="tray__swatch"
    :style="{ background: `#${color.color}` }"
  ></div>
</template>
<script>
export default {
  name: "ColorOption",
  props: {
    color: Object,
  },
};
</script>
