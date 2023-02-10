<template>
    <div>
        <h3>-- Product List --</h3>
        <p v-if="products.length==0">Product List is empty</p>
        <table class="table">
            <thead>
                <tr>
                    <th>Id</th>
                    <th>Product Name</th>
                    <th>Category</th>
                    <th>Description</th>
                    <th>Unit Price</th>
                    <th>Unit in Stock</th>
                    <th></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="product in products" :key="product.id">
                    <td>{{product.id}}</td>
                    <td>{{product.productName}}</td>
                    <td>{{product.categoryId}}</td>
                    <td>{{product.queantityPerUnit}}</td>
                    <td>{{product.unitPrice}}</td>
                    <td>{{product.unitInStock}}</td>
                    <td><button class="btn btn-sm btn-danger" @click="handleDelete(product)">Delete</button></td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name: "product-list",
    props:{
        products:Array
    },
    methods:{
        handleDelete(product){
            this.$emit("delete:product",product)
        }
    }
};
</script>

<style scoped>

</style>