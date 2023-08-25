<template>
  <div>
    <h1>Ürün Listesi</h1>
    <div v-if="loading">Loading...</div>
    <table v-else>
      <thead>
        <tr>
          <th>Ürün Adı</th>
          <th>Fiyat</th>
          <th>Kategori</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td>{{ product.title }}</td>
          <td>{{ product.price }}</td>
          <td>{{ product.category }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loading: true, 
      products: []
    };
  },
  async mounted() {
    try {
      const response = await fetch('https://fakestoreapi.com/products'); 
      const json = await response.json();
      this.products = json;
      this.loading = false; 
    } catch (error) {
      console.error('API isteği sırasında hata oluştu:', error);
      this.loading = false; 
    }
  }
};
</script>

<style>
table {
  border-collapse: collapse;
  width: 100%;
}

th, td {
  border: 1px solid black;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
}
</style>
