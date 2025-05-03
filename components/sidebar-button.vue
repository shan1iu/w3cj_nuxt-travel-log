<script setup lang="ts">
const props = defineProps<{
  label: string;
  icon: string;
  href: string;
  showLabel: boolean;
}>();
const route = useRoute();
</script>

<template>
  <div
    class="tooltip tooltip-right"
    :data-tip="props.showLabel ? undefined : props.label"
  >
    <NuxtLink
      class="flex flex-nowrap gap-2 p-2 hover:bg-base-300 cursor-pointer"
      :to="props.href"
      :class="{
        'bg-base-200': route.path === props.href,
        'justify-center': !props.showLabel,
        'justify-start': props.showLabel,
      }"
    >
      <Icon :name="props.icon" size="24" />
      <Transition name="grow">
        <span v-if="showLabel">
          {{ props.label }}
        </span>
      </Transition>
    </NuxtLink>
  </div>
</template>

<style scoped>
.grow-enter-active {
  animation: grow 0.2s;
}
.grow-leave-active {
  animation: grow 0.2s reverse;
}
@keyframes grow {
  0% {
    transform: scale(0);
  }
  100% {
    transform: scale(1);
  }
}
</style>
