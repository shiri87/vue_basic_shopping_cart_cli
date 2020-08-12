<template>
  <transition
    name="custom"
    enter-active-class="animated fadeInDown"
    leave-active-class="animated slideOutRight"
  >
    <div v-if="sliderStatus">
      <div class="align-items-center" v-bind:class="sliderState">
        <label v-bind:class="labelArray" for="formMax">Max</label>
        <input
          type="text"
          class="form-control mx-2"
          v:bind:style="{'width': inputWidth + 'px', 'text-align':'center'}"
          id="formMax"
          v-model:value="maxAmount"
          @change="$emit('update:maximum',maxAmount)"
        />
        <input
          type="range"
          class="custom-range my-3"
          min="0"
          max="200"
          v-model:value="maxAmount"
          @change="$emit('update:maximum',maxAmount)"
        />
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "price-slider",
  props: ["sliderStatus"],
  data: function () {
    return {
      maxAmount: 99,
    };
  },
  computed: {
    sliderState: function () {
      return this.sliderStatus ? "d-flex" : "d-none";
    },
  },
};
</script>

<style>
</style>