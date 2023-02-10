<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld :msg="54"/>
  <div id="app">
    <ProductAdd @add:product="addProduct"/>
    <ProductList @delete:product="deleteProduct" @update:product="updateProduct" :products="products" />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import ProductList from './components/ProductList.vue';
import ProductAdd from './components/ProductAdd.vue';

export default {
  name: 'App',
  components: {
    HelloWorld,ProductList,ProductAdd
  },
  data(){
    return {
      products:[
        {id:1,categoryId:1,productName:'Laptop',queantityPerUnit:'Acer Laptop',unitPrice:5000,unitInStock:2},
        {id:2,categoryId:2,productName:'Maouse',queantityPerUnit:'Gaming Maouse',unitPrice:600,unitInStock:3},
        {id:3,categoryId:3,productName:'Keyboard',queantityPerUnit:'Gaming Keyboard',unitPrice:78,unitInStock:5},
      ]
    }
  },
  methods:{
    deleteProduct(product){
      this.products=this.products.filter(
        productToFilter=>productToFilter.id!==product.id
      )
    },
    updateProduct(){

    },
    addProduct(product){
      const newProduct={...product} // new reference
      this.products={...this.products,newProduct}
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
