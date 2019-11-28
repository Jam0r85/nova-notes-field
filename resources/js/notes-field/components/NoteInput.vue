<template>
  <div class="bg-20 w-3/5 p-4 flex border-t border-40">
    <textarea
      rows="3"
      :placeholder="placeholder"
      class="w-full form-control form-input form-input-bordered py-3 h-auto"
      v-bind:value="value"
      v-on:input="$emit('input', $event.target.value)"
    />

    <div class="whitespace-no-wrap ml-2">
      <button
        class="btn btn-default btn-primary inline-flex items-center relative ml-auto"
        @click="$emit('onSubmit')"
        :disabled="loading"
      >
        Add note
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['placeholder', 'value', 'loading'],
};
</script>
