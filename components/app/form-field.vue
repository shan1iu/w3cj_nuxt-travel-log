<script setup lang="ts">
const props = defineProps<{
  label: string;
  name: string;
  error?: string;
  type?: "text" | "textarea" | "number";
  disabled?: boolean;
}>();
const asField = computed(() => {
  if (props.type) {
    if (props.type === "number") {
      return "input";
    }
    else {
      return props.type;
    }
  }
  else {
    return "input";
  }
});
</script>

<template>
  <fieldset class="fieldset">
    <legend class="fieldset-legend">
      {{ props.label }}
    </legend>
    <Field
      :as="asField"
      :name="props.name"
      :type="props.type || 'text'"
      :disabled="props.disabled"
      class="w-full"
      :class="{
        'input-error': props.error,
        'input': !props.type || props.type === 'text' || props.type === 'number',
        'textarea': props.type === 'textarea',
      }"
    />
    <p v-if="props.error" class="label text-error">
      {{ props.error }}
    </p>
  </fieldset>
</template>
