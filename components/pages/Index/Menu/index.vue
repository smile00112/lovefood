<template>
  <section class="index-menu">
    <div class="container">
      <PagesIndexMenuCategories
        @show-filters="isShowFilters = true"
        class="index-menu__categories"
      />

      <div class="index-menu__content">
        <div
          v-for="block in catalog.catalog"
          :key="block.id"
          :id="`block_${block.id}`"
          class="index-menu__block"
        >
          <h2 class="index-menu__title">
            {{ block.name }}
          </h2>
          <div class="index-menu__list">
            <CommonProductCard
              v-for="product in block.products"
              :key="product.id"
              :item="product"
            />
          </div>
        </div>
      </div>
    </div>

    <ModalsFilters
      v-if="isShowFilters"
      @close="isShowFilters = false"
    />
  </section>
</template>

<script setup>
import { useCatalogStore } from '@/store/catalog'

const catalog = useCatalogStore()

const isShowFilters = ref(false)
</script>

<style lang="scss" scoped>
.index-menu {
  &__categories {
    margin-bottom: 30px;

    @include mq($bp-small) {
      margin-bottom: 40px;
    }
  }

  &__content {
    display: flex;
    flex-direction: column;
  }

  &__block {
    display: flex;
    flex-direction: column;
    grid-gap: 20px;

    margin-bottom: 20px;

    @include mq($bp-small) {
      grid-gap: 30px;

      margin-bottom: 30px;
    }

    &:last-child {
      margin-bottom: 0;
    }
  }

  &__title {
    @include text_large;
    font-weight: 700;

    @include mq($bp-small) {
      @include h2;
    }
  }

  &__list {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-gap: 16px;

    @include mq($bp-small) {
      grid-template-columns: repeat(5, 1fr);
      grid-gap: 30px 17px;
    }
  }
}
</style>