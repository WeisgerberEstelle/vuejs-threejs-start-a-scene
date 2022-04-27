<template>
  <div class="controls">
    <div id="js-tray" class="tray">
      <div id="js-tray-slide" class="tray__slide">
        <div :key="color.color" v-for="color in colors">
          <ColorOption
            :color="color.color"
            @color-click="$emit('ChoseAColor')"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ColorOption from "./ColorOption";
export default {
  name: "ListColors",
  props: {
    colors: Array,
  },
  components: {
    ColorOption,
  },
};
</script>
