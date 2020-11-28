<template>
  <div class="add-modal">
    <h3 class="add-modal__header">Add new car</h3>
    <div class="add-modal__form">
      <AppInput
        :errors="$v.form.title"
        :isInvalid="$v.form.title.$error"
        label="Title"
        @blur="$v.form.title.$touch()"
        errorMessage="Title is required"
        errorTypeMessage="The field must contain only alphabetic characters, spaces, and hyphens"
        placeholder="Title"
        required
        type="text"
        v-model="form.title"
      />
      <AppInput
        :errors="$v.form.price"
        :isInvalid="$v.form.price.$error"
        label="Price"
        @blur="$v.form.price.$touch()"
        errorMessage="Price is required"
        errorTypeMessage="The field must contain numbers"
        placeholder="Price"
        required
        type="text"
        v-model="form.price"
      />
      <AppInput
        :errors="$v.form.imageUrl"
        :isInvalid="$v.form.imageUrl.$error"
        label="Image Url"
        @blur="$v.form.imageUrl.$touch()"
        errorMessage="Image Url is required"
        errorTypeMessage="The field must contain url"
        placeholder="Image Url"
        type="text"
        v-model="form.imageUrl"
      />
      <div class="add-modal__form--fields">
        <AppInput
          :errors="$v.form.persons"
          :isInvalid="$v.form.persons.$error"
          label="Persons"
          @blur="$v.form.persons.$touch()"
          errorMessage="Persons is required"
          errorTypeMessage="The field must contain numbers"
          placeholder="Persons"
          required
          type="text"
          v-model="form.persons"
        />
        <AppInput
          :errors="$v.form.doors"
          :isInvalid="$v.form.doors.$error"
          label="Doors"
          @blur="$v.form.doors.$touch()"
          errorMessage="Doors is required"
          errorTypeMessage="The field must contain numbers beetwen 2 and 8"
          placeholder="Doors"
          required
          type="text"
          v-model="form.doors"
        />
        <AppInput
          :errors="$v.form.litres"
          :isInvalid="$v.form.litres.$error"
          label="Litres per 100 km"
          @blur="$v.form.litres.$touch()"
          errorMessage="Litres per 100 km is required"
          errorTypeMessage="The field must contain numbers"
          placeholder="Litres per 100 km"
          required
          type="text"
          v-model="form.litres"
        />
      </div>
      <AppInput
          :errors="$v.form.description"
          :isInvalid="$v.form.description.$error"
          label="Description"
          @blur="$v.form.description.$touch()"
          errorMessage="Description is required"
          errorTypeMessage="The field must contain only alphabetic characters, spaces, and hyphens"
          placeholder="Description"
          type="textarea"
          v-model="form.description"
        />
    </div>

    <div class="add-modal__buttons">
      <button class="button__primary" @click="close">
        Cancel
      </button>
      <button class="button__secondary" @click="additem">
        Submit
      </button>
    </div>
  </div>
</template>

<script>
import { required, minLength, maxLength, between, alphaNum } from 'vuelidate/lib/validators'

import AppInput from '@/components/AppInput'

export default {
  name: 'AddModal',

  components: {
    AppInput
  },

  data: () => ({
    form: {
      title: '',
      price: '',
      imageUrl: '',
      persons: '',
      doors: '',
      litres: '',
      description: '',
    },
  }),

  validations: {
    form: {
      title: {
        required,
        minLength: minLength(3),
        maxLength: maxLength(60)
      },
      imageUrl: {
        required,
      },
      price: {
        required,
        alphaNum,
        alpha: value => !value.match(/[^0-9 ]/),
      },
      persons: {
        required,
        alphaNum,
        alpha: value => !value.match(/[^0-9 ]/),
      },
      doors: {
        required,
        alphaNum,
        between: between(2, 8)
      },
      litres: {
        required,
        alphaNum,
        alpha: value => !value.match(/[^0-9 ]/),
      },
      description: {
        minLength: minLength(40)
      },
    }
  },
  methods: {
    additem() {
      this.$v.form.$touch()

      if (this.$v.form.$invalid) {
        return;
      }

      // const payload = { title: this.title };


      this.$emit("add-item", this.form);
    },
    close() {
      this.$emit("close-item");
    }
  }
};
</script>

<style scoped lang="scss">
  .add-modal {
    border-radius: 10px;
    background: #fff;
    position: absolute;
    position: absolute;
    top: 10%;
    left: 50%;
    transform: translateX(-50%);
    box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
    width: 80%;
    margin: 0 auto;
  }

  .add-modal__header {
    padding: 40px 30px;
  }

  .add-modal__form {
    padding: 40px 30px 0px 30px;
  }

  .add-modal__header {
    font-size: 26px;
    color: $ebonyClay;
    border-bottom: 1px solid $silverChalice;
    line-height: 1;
  }

  .add-modal__form {
    overflow: hidden;
  }

  .add-modal__form--fields {
    display: flex;

    @media (max-width: $breakpoint-tablet-ls) {
      flex-wrap: wrap;
    }

    @media (min-width: $breakpoint-tablet-ls + 1) {
      justify-content: space-between;
      margin-left: -30px;
    }

    .app-input {
      @media (max-width: $breakpoint-tablet-ls) {
        width: 100%;
      }

      @media (min-width: $breakpoint-tablet-ls + 1) {
        width: calc(100% - 30px);
        margin-left: 30px;
      }
    }
  }

  .add-modal__buttons {
    display: flex;
    justify-content: space-between;
    padding: 0 30px 30px 30px;
  }
</style>