<template>
  <div id="productList">
    <p v-if="products.length==0">Product list is empty!</p>
    <table v-else class="table">
      <thead>
        <tr>
          <th>ID</th>
          <th>Product Name</th>
          <th>Category</th>
          <th>Description</th>
          <th>Unit Price</th>
          <th>Stock #</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td v-if="updateId===product.id">
            <input v-model="product.id" type="text" class="form-control" id="id" />
          </td>
          <td v-else>{{product.id}}</td>
          <td v-if="updateId===product.id">
            <input v-model="product.productName" type="text" class="form-control" id="productName" />
          </td>
          <td v-else>{{product.productName}}</td>
          <td v-if="updateId===product.id">
            <input v-model="product.categoryId" type="text" class="form-control" id="categoryId" />
          </td>
          <td v-else>{{product.categoryId}}</td>
          <td v-if="updateId===product.id">
            <input
              v-model="product.quantityPerUnit"
              type="text"
              class="form-control"
              id="quantityPerUnit"
            />
          </td>
          <td v-else>{{product.quantityPerUnit}}</td>
          <td v-if="updateId===product.id">
            <input v-model="product.unitPrice" type="text" class="form-control" id="unitPrice" />
          </td>
          <td v-else>{{product.unitPrice}}</td>
          <td v-if="updateId===product.id">
            <input
              v-model="product.unitsInStock"
              type="text"
              class="form-control"
              id="unitsInStock"
            />
          </td>
          <td v-else>{{product.unitsInStock}}</td>

          <td v-if="updateId!==product.id">
            <button class="btn btn-small btn-primary" @click="handleUpdate(product)">Update</button>
            <button class="btn btn-small btn-danger" @click="handleDelete(product)">Delete</button>
          </td>
          <td v-else>
            <button class="btn btn-small btn-primary" @click="handleSave(product)">Save</button>
            <button class="btn btn-small btn-danger" @click="updateId=null">Cancel</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "product-list",
  data() {
    return { updateId: null };
  },
  props: {
    products: Array
  },
  methods: {
    handleDelete(product) {
      this.$emit("delete:product", product);
    },
    handleUpdate(product) {
      this.updateId = product.id;
    },
    handleSave(product) {
      this.$emit("update:product", product);
      this.updateId = null;
    }
  }
};
</script>

<style scoped>
#productList {
  margin: 24px;
}
.btn {
  margin-left: 12px;
  margin-bottom: 6px;
  float: right;
  width: 80px;
}
table {
  width: 100%;
  border-collapse: collapse;
}
/* Zebra striping */
tr:nth-of-type(odd) {
  background: #eee;
}
th {
  background: #333;
  color: white;
  font-weight: bold;
}
td,
th {
  padding: 6px;
  border: 1px solid #ccc;
  text-align: left;
}
@media only screen and (max-width: 760px),
  (min-device-width: 768px) and (max-device-width: 1024px) {
  /* Force table to not be like tables anymore */
  table,
  thead,
  tbody,
  th,
  td,
  tr {
    display: block;
  }

  /* Hide table headers (but not display: none;, for accessibility) */
  thead tr {
    position: absolute;
    top: -9999px;
    left: -9999px;
  }

  tr {
    border: 1px solid #ccc;
  }

  td {
    /* Behave  like a "row" */
    border: none;
    border-bottom: 1px solid #eee;
    position: relative;
    padding-left: 50%;
  }

  td:before {
    /* Now like a table header */
    position: absolute;
    /* Top/left values mimic padding */
    top: 6px;
    left: 6px;
    width: 45%;
    padding-right: 10px;
    white-space: nowrap;
  }
  table td:last-child {
    height: 60px;
  }
  .btn {
    float: left;
    margin: 0 12px 0 0;
  }
}
</style>