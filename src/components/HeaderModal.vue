<template>
  <header>
    <div class="header__wrapper">
      <h1 class="title">Cars2go</h1>
      <button class="header__button" @click="$emit('handle-modal-active', true)">
        Add new car
      </button>
    </div>
  </header>
</template>

<script>
export default {
  name: "HeaderModal",
};
</script>

<style lang="scss">
  header {
    font-family: $font-body;
    background: $ebonyClay;
  }

  .header__wrapper {
    padding: 25px 20px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .title {
    font-size: 24px;
    font-weight: 500;
    color: $color-light-text;
  }

  .header__button {
    cursor: pointer;
    color: $color-light-text;
    font-weight: 300;
    font-size: 14px;
  }
</style>