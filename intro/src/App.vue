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
      products:[]
    }
  },
  mounted(){
    this.getProducts()
  },
  methods:{
   async getProducts(){
      const result=await fetch('http://localhost:3000/products')
      const data = await result.json()
      this.products=data;
    },
    async deleteProduct(product){
      await fetch('http://localhost:3000/products',{
        method:'DELETE'
      })
      this.products=this.products.filter(
        productToFilter=>productToFilter.id!==product.id
      )
    },
    async updateProduct(product){
      const result=await fetch('http://localhost:3000/products/'+product.id,{
        method:'PUT',
        body:JSON.stringify(product),
        headers:{"Content-Type":"application/json"}
      })
      const updatedProduct=await result.json()
      this.products=this.products.map(product=>product.id==updatedProduct.id?updatedProduct:product)
    },
    async addProduct(product){
      const result=await fetch('http://localhost:3000/products',{
        method:'POST',
        body:JSON.stringify(product),
        headers:{"Content-Type":"application/json"}
      })
      const newProduct= await result.json() // post 
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
