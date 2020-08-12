<template>
  <span>
    {{
    this.prefix +
    Number.parseFloat(value * this.conversion).toFixed(this.precision)
    }}
  </span>
</template>

<script>
export default {
  props: {
    value: Number,
    prefix: { type: String, default: "Gold : ", require: true },
    precision: { type: Number, default: 2 },
    conversion: { type: Number, default: 1 },
  },
};
</script>

<style></style>
