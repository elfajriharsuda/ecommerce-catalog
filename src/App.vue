<template>
  <div id="app">
    <HeaderSection /> 
    <ProductDisplay />
    <FooterSection />
  </div>
</template>

<script>
import HeaderSection from './components/HeaderSection.vue'
import ProductDisplay from './components/ProductDisplay.vue'
import FooterSection from './components/FooterSection.vue' 

export default {
  name: 'App',
  components: {
    HeaderSection,
    ProductDisplay,
    FooterSection,
  }
}
</script>
  
<style>
</style>