<template>
  <div class="container">
    <div v-if="isLoading" class="card">
      <div class="product-container">
        <div class="loader-container">
          <div class="loader"></div>
        </div>
      </div>
    </div>
    <div v-else class="container"
      :class="
        !isProductAvailable
          ? 'bg-light-gray'
          : product.data.category === 'men\'s clothing'
          ? 'bg-light-blue'
          : 'bg-light-pink'
      ">
      <div class="overlay">
        <img src="../assets/bg-shape.svg" alt="background overlay" />
      </div>
      <div class="card">
        <div v-if="!isProductAvailable" class="product-unavailable">
          <div class="overlay">
            <img src="../assets/bg-sad.svg" alt="Product Unavailable" />
          </div>
          <div class="product-details">
            <p>This product is unavailable to show</p>
            <div class="button-container">
              <button type="button" @click="getSingleProduct()" class="btn-next">
                Next Product
              </button>
            </div>
          </div>
        </div>
        <div v-else class="product-container">
          <div class="product-image">
            <img :src="product.data.image" alt="Product Image" />
          </div>
          <div class="product-details">
            <div class="product-title">
              <h3
                :class="
                  product.data.category === 'men\'s clothing'
                    ? 'font-dark-blue'
                    : 'font-dark-pink'
                "
                class="title">
                {{ product.data.title }}
              </h3>
              <div class="product-sub-title">
                <span>{{ product.data.category }}</span>
                <div class="rating">
                  <span>{{ product.data.rating.rate }}/5</span>
                  <div class="circle-container">
                    <div v-for="i in 5" :key="i" 
                      :class="[
                        i <= product.data.rating.rate 
                        ? (product.data.category === 'men\'s clothing' 
                          ? 'circle-dark-blue' 
                          : 'circle-dark-pink') 
                        : 'circle-filled',
                        ]"
                        class="circle">
                    </div>
                  </div>
                </div>
              </div>
              <div class="description">
                <p>{{ product.data.description }}</p>
              </div>
            </div>
            <div class="price-color">
              <span
                :class="
                  product.data.category === 'men\'s clothing'
                    ? 'font-dark-blue'
                    : 'font-dark-pink'
                "
                class="price">${{ product.data.price }}</span>
              <div class="button-container">
                <button
                  type="button"
                  :class="
                    product.data.category === 'men\'s clothing'
                      ? 'bg-dark-blue'
                      : 'bg-dark-pink'
                  "
                  class="btn-buy">
                  Buy Now
                </button>
                <button
                  type="button"
                  @click="getSingleProduct()"
                  :class="
                    product.data.category === 'men\'s clothing'
                      ? 'border-btn-dark-blue font-dark-blue'
                      : 'border-btn-dark-pink font-dark-pink'
                  "
                  class="btn-next">
                  Next Product
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
</div>
  
</template>
<script>
export default {
  name: 'ProductDisplay',
  data () {
    return {
      isLoading: false,
      index: 0,
      isProductAvailable: false,
      product: {}
    }
  },
  methods: {
    async callAPI () {
      const response = await fetch(
        `https://fakestoreapi.com/products/${this.index}`
      )
      const result = await response.json()
      console.log(result)
      return result
    },
    async getSingleProduct () {
      this.isLoading = true

      this.index == 20 ? (this.index = 1) : this.index++

      let data = await this.callAPI()
      if (
        data.category === "men's clothing" ||
        data.category === "women's clothing"
      ) {
        this.product = { data }
        this.isProductAvailable = true
      } else {
        this.isProductAvailable = false
      }
      this.isLoading = false
    }
  },

  mounted () {
    this.getSingleProduct()
  }
}
</script>
<style>
@import '../assets/style/style.css';
</style>
