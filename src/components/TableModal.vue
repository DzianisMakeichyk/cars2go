<template>
  <section>
    <ul class="list">
      <template>
        <li
          v-for="item in items"
          :key="item.id"
          class="item"
        >
          <div class="item__wrapper">
            <!-- Image -->
            <div class="item__image">
              <div class="item-image__wrapper">
                <img :src="item.imageUrl" role="presentation">
              </div>
            </div>
            <!-- Description -->
            <div class="item__description">
              <div class="item__description__wrapper">
                <h2 class="item-description__title">{{ item.title }}</h2>
                <div class="item-spec">
                  <div class="item-spec__elem">🧍{{ item.persons }}</div>
                  <div class="item-spec__elem">🚪{{ item.doors }}</div>
                  <div class="item-spec__elem">🛢️{{ item.litres }}/100km</div>
                </div>

              <div class="item-description">
                  <div class="item-description__offer">
                    <p class="item-description__sub-title">Description</p>
                    <p class="item-description__copy">
                      {{ item.description }}
                    </p>
                  </div>
                  <div class="item-description__toolbar">
                    <div class="item-toolbar">
                      <div class="item-toolbar__price">${{ item.price }}</div>
                      <div class="item-toolbar__buttons">
                        <button class="item-toolbar__button--primary">Book Now</button>
                        
                        <button
                          class="item-toolbar__button--secondary"
                          @click="$emit('delete-item', item.row)"
                        >
                          Delete car
                        </button>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </li>
      </template>
    </ul>
  </section>
</template>

<script>

export default {
  name: 'TableModal',
  props: {
    items: {
      type: Array,
      required: true
    }
  },
};
</script>

<style lang="scss" scoped>
  .item {
    border: 10px solid $wildSand;
    padding: 30px;
  }

  .item + .item {
    border-top: 15px solid $wildSand;
  }

  .item__wrapper {
    display: flex;
    align-items: center;
    justify-content: space-between;

    @media (max-width: $breakpoint-tablet-ls) {
      flex-direction: column;
    }
  }

  .item__image {
    width: 100%;

    @media (max-width: $breakpoint-tablet-ls) {
      margin-bottom: 30px;
    }

    @media (min-width: $breakpoint-tablet-ls + 1) {
      width: 40%;
    }
  }

  .item-image__wrapper {
    overflow: hidden;
    padding-top: 200 / 340 * 100%;
    position: relative;

    @media (min-width: $breakpoint-tablet-ls + 1) {
      margin: 0 20px 0 0;
    }

    img {
      height: 100%;
      position: absolute;
      right: 0;
      top: 0;
      width: 100%;
    }
  }

  .item__description {
    @media (min-width: $breakpoint-tablet-ls + 1) {
      width: 60%;
    }
  }

  .item__description__wrapper {
    @media (min-width: $breakpoint-tablet-ls + 1) {
      margin: 0 0 0 20px;
    }
  }

  .item-description__title {
    font-size: 32px;
    color: $color-text;
    font-weight: 500;
    padding-bottom: 25px;

    @media (max-width: $breakpoint-tablet-ls) {
      font-size: 22px;
    }
  }

  .item-description__copy {
    font-size: 16px;
    font-weight: 300;
    line-height: 1.4;
    color: $color-grey-text;
  }

  .item-description__sub-title {
    font-size: 18px;
    color: $color-text;
    font-weight: 500;
    padding-bottom: 9px;
  }

  .item-spec {
    display: flex;
    align-items: center;
    justify-content: flex-start;
    margin-bottom: 20px;
  }

  .item-spec__elem {
      font-size: 12px;
      color: $color-text;
      font-weight: 500;
      margin: 0 6px 0 0;
      padding: 6px 5px;
      border: 1px solid $silverChalice;
      border-radius: 4px;
      line-height: 1;
  }

  .item-description {
    display: flex;
    align-items: center;
    justify-content: space-between;

    @media (max-width: $breakpoint-phone) {
      flex-direction: column;
    }
  }

  .item-description__offer {
    width: 100%;

    @media (max-width: $breakpoint-phone) {
      padding: 0 0 30px 0;
    }

    @media (min-width: $breakpoint-phone + 1) {
      padding: 0 30px 0 0;
      min-height: 120px;
      border-right: 1px solid $silverChalice;
    }
  }

  .item-description__toolbar {
    @media (min-width: $breakpoint-phone + 1) {
      padding: 0 0 0 30px;
    }
  }

  .item-toolbar__price {
    font-size: 44px;
    color: $color-green-price;
    font-weight: 500;

    @media (max-width: $breakpoint-phone) {
      text-align: center;
      padding: 0 0 15px 0;
    }

    @media (min-width: $breakpoint-phone + 1) {
      padding: 0 20px 11px 0;
    }
  }

  .item-toolbar__buttons {
    display: flex;
    flex-direction: column;

    button {
      line-height: 1;
      cursor: pointer;
      white-space: nowrap;
    }

    button + button {
      margin: 8px 0 0 0;
    }
  }

  .item-toolbar__button--primary {
    background: $ebonyClay;
    color: $color-light-text;
    font-weight: 500;
    font-size: 22px;
    padding: 13px 35px;
  }

  .item-toolbar__button--secondary {
    color: $color-grey-text;
    font-size: 10px;
  }
</style>