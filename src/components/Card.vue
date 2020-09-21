<template>
  <div class="text-center p-4">
    <p
      class="text-xs text-gray-500 font-semibold uppercase leading-none tracking-wider"
    >
      {{ title }}
    </p>
    <h3 class="mt-1 text-xl text-gray-900 font-medium">{{ body }}</h3>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    title: {
      type: String,
      required: true
    },
    body: {
      type: String,
      required: true
    }
  },
  data() {
    return {};
  }
};
</script>

<style lang="css" scoped></style>
