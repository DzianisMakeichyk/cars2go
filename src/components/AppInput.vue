<template>
  <div class="app-input">
    <div class="app-input__content">
      <label :for="placeholder.replace(' ', '-')">
        {{ label }}
      </label>
      <input
        v-if="type !== 'textarea'"
        class="app-input__inner"
        :type="type"
        :placeholder="placeholder"
        @input="$emit('input', value)"
        @change="$emit('input', value)"
        @blur="$emit('blur')"
        v-model="value"
        :disabled="disabled"
        :id="placeholder.replace(' ', '-')"
        :name="placeholder.replace(' ', '-')"
      >

      <textarea
        v-if="type === 'textarea'"
        class="app-input__inner app-input__inner--textarea"
        :placeholder="placeholder"
        @input="$emit('input', value)"
        @change="$emit('input', value)"
        v-model="value"
      ></textarea>

      <div class="app-input__errors" v-if="isInvalid">
          <small v-if="!required">{{ errorMessage }}</small>

          <small v-else-if="!isErrorType">{{ errorTypeMessage }}</small>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    type: {
      type: String,
      default: '',
    },

    placeholder: {
      type: String,
      default: '',
    },

    label: {
      type: String,
      default: ''
    },
    
    errorMessage: {
      type: String,
      default: ''
    },
    
    errorTypeMessage: {
      type: String,
      default: ''
    },

    required: {
      type: Boolean,
      default: false
    },

    isErrorType: {
      type: Boolean,
      default: false
    },

    isInvalid: {
      type: Boolean,
      default: false
    },

    disabled: {
      type: Boolean,
      default: false
    },

    defaultValue: {
      type: String,
      default: ''
    },
  },

  data: () => ({
    value: '',
  }),

  mounted() {
    this.value = this.defaultValue ? this.defaultValue : this.value;
  },
}
</script>

<style lang="scss" scoped>
  .app-input {
    input,
    textarea {
      font-weight: 15px;
      width: 100%;
      padding: 7px 10px;
      border-radius: 5px;
      border: 1px solid $wildSand;
      line-height: 1;
      box-sizing: border-box;

      &::placeholder {
        color: $silverChalice;
      }
    }

    textarea {
      min-height: 300px;
    }

    label {
      font-size: 14px;
      color: $color-text;
      margin-bottom: 5px;
      display: block;
    }
  }

  .app-input__content {
    padding-bottom: 25px;
    position: relative;
  }

  .app-input__errors {
    position: absolute;
    left: 5px;
    bottom: 10px;
    font-size: 13px;
    color: red;
    white-space: nowrap;
  }
</style>
