<template>
  <div>
    <input
      :id="id"
      v-model="val"
      class="form-control"
      :class="getType"
      :name="name"
      placeholder="…"
      type="text"
      :disabled="disabled == 1"
    />
  </div>
</template>

<script>
import field from '../mixins/value';

export default {
  name: 'EditorText',
  mixins: [field],
  props: ['value', 'label', 'name', 'type', 'disabled', 'id'],
  data: () => {
    return {
      generate: false,
    };
  },
  computed: {
    getType() {
      if (this.type === 'large') {
        return 'form-control-lg';
      }

      return '';
    },
  },
  watch: {
    val() {
      if (this.generate) {
        this.$root.$emit('slugify-from-title');
      }
    },
  },
  mounted() {
    this.$root.$on('generate-from-title', data => (this.generate = data));
  },
};
</script>
