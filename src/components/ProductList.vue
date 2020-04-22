<template>
  <div>
    <p v-if="products.length==0">Product list is empty!</p>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Product Name</th>
          <th>Category</th>
          <th>Description</th>
          <th>Unit Price</th>
          <th>Stock #</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td>{{product.id}}</td>
          <td>{{product.productName}}</td>
          <td>{{product.categoryId}}</td>
          <td>{{product.quantityPerUnit}}</td>
          <td>{{product.unitPrice}}</td>
          <td>{{product.unitsInStock}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "product-list",
  props: {
    products: Array
  }
};
</script>

<style scoped>
</style>