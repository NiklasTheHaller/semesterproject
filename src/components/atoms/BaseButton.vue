<template>
  <button
    class="rounded-md py-2.5 px-4 text-center font-medium transition-all duration-300 disabled:opacity-50 disabled:cursor-not-allowed"
    :class="buttonClass"
    @click="onClick"
  >
    <slot />
  </button>
</template>

<script setup>
  import { computed, defineProps } from "vue";

  const props = defineProps({
    variant: {
      type: String,
      default: "primary",
      validator: (value) =>
        ["primary", "secondary", "ghost", "outline"].includes(value),
    },
    onClick: {
      type: Function,
      default: () => {},
    },
  });

  const buttonClass = computed(() => {
    switch (props.variant) {
      case "ghost":
        return "hover:bg-neutral-100 text-neutral-600";
      case "outline":
        return "border border-neutral-400 text-neutral-600 hover:bg-neutral-200 hover:text-neutral-700";
      case "secondary":
        return "bg-secondary-600 text-neutral-100 border border-secondary-700 hover:bg-secondary-700 shadow-sm hover:shadow-md";
      default:
        return "bg-primary-600 text-neutral-100 border border-primary-700 hover:bg-primary-700 shadow-sm hover:shadow-md";
    }
  });
</script>
