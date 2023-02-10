<template>
    <div id="list">
        <h3>-- Product List --</h3>
        <p v-if="products.length==0">Product List is empty</p>
        <table v-else class="table">
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
                    <td v-if="updateId==product.id"><input v-model="product.id" type="text" class="form-control" id="id"></td>
                    <td v-else>{{ product.id }}</td>
                    <td v-if="updateId==product.id"><input v-model="product.productName" type="text" class="form-control" id="id"></td>
                    <td v-else>{{ product.productName }}</td>
                    <td v-if="updateId==product.id"><input v-model="product.categoryId" type="text" class="form-control" id="id"></td>
                    <td v-else>{{ product.categoryId }}</td>
                    <td v-if="updateId==product.id"><input v-model="product.queantityPerUnit" type="text" class="form-control" id="id"></td>
                    <td v-else>{{ product.queantityPerUnit }}</td>
                    <td v-if="updateId==product.id"><input v-model="product.unitPrice" type="text" class="form-control" id="id"></td>
                    <td v-else>{{ product.unitPrice }}</td>
                    <td v-if="updateId==product.id"><input v-model="product.unitInStock" type="text" class="form-control" id="id"></td>
                    <td v-else>{{ product.unitInStock }}</td>
                    <td v-if="updateId!==product.id">
                        <button class="btn btn-sm btn-primary" @click="handleEdit(product)">Edit</button>
                        <button class="btn btn-sm btn-danger" @click="handleDelete(product)">Delete</button>
                    </td>
                    <td v-else>
                        <button class="btn btn-sm btn-primary" @click="handleUpdate(product)">Update</button>
                        <button class="btn btn-sm btn-danger" @click="updateId=null">Cancel Update</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name: "product-list",
    data(){
        return {updateId:null};
    },
    props:{
        products:Array
    },
    methods:{
        handleDelete(product){
            this.$emit("delete:product",product)
        },
        handleEdit(product){
            this.updateId=product.id
        },
        handleUpdate(product){
            this.$emit("update:product",product)
            this.updateId=null
        }

    }
};
</script>

<style scoped>
#list{
    margin: 100px;
}
</style>