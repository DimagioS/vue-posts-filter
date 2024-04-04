<template>
  <div class="container">
    <div class="row justify-content-center mb-3">
      <div class="my-1">
        <div class="input-group">
          <span class="input-group-text input-img" id="basic-addon1">
            <img src="../assets/icons/magnifying-glass.svg" alt="magnifying-glass">
          </span>
          <input 
            type="text"
            class="form-control" 
            placeholder="Filter by author..."
            :value="modelValue"
            @input="$emit('update:modelValue', $event.target.value)"
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    modelValue: {
      type: String,
      required: true
    }
  },
  emits: ['update:modelValue'],
}
</script>

<style lang="scss" src="../styles/authorFilter.scss" scoped></style>