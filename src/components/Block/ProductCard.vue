<script setup lang="ts">
import CardBrand from "../Ui/CardBrand.vue";
import CardCategory from "../Ui/CardCategory.vue";
import CardDescription from "../Ui/CardDescription.vue";
import CardDiscount from "../Ui/CardDiscount.vue";
import CardPrice from "../Ui/CardPrice.vue";
import CardRating from "../Ui/CardRating.vue";
import CardTitle from "../Ui/CardTitle.vue";
import CardThumbnail from "../Ui/CardThumbnail.vue";

interface Product {
  id: number;
  title: string;
  description: string;
  price: number;
  category: string;
  discountPercentage: number;
  rating: number;
  brand: string;
  thumbnail: string;
}

const props = defineProps<{
  product: Product;
}>();
</script>

<template>
  <div class="product__card">
    <div class="product__card_img-container">
      <CardThumbnail :src="product.thumbnail" :alt="product.title" />
    </div>

    <div class="product__card_description">
      <CardTitle :text="product.title" />
      <CardDescription :text="product.description" />

      <div class="product__card_description-info">
        <CardDiscount :text="product.discountPercentage" />
        <CardBrand :text="product.brand" />
      </div>

      <div class="product__card_description-additional-info">
        <CardPrice :text="product.price" />
        <CardRating :text="product.rating" />
        <CardCategory :text="product.category" />
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.product__card {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 35px 40px;
  width: 100%;
  background: rgba(255, 255, 255, 0.3);
  border-radius: 16px;
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(5.6px);
  border: 1px solid rgba(255, 255, 255, 0.28);

  &_img-container {
    width: 300px;
  }

  &_description {
    display: flex;
    flex-direction: column;
    gap: 10px;

    &-info {
      display: flex;
      align-items: center;
      gap: 40px;
    }

    &-additional-info {
      margin-top: 20px;
      display: flex;
      align-items: center;
      gap: 40px;
    }
  }
}

@media (max-width: 767px) {
  .product__card {
    flex-direction: column;
  }
}
</style>
