<template>
<div>
    <h2>Tooted</h2>
    <b-table striped hover :items="productItems" :fields="productFields">
         <template #cell(price)="data">
        <b class="text-info">{{ data.value}} EUR</b>
         </template>
    </b-table>

        </div>
    
</template>

<script>
import axios from 'axios';
export default {
    name:'products',

    data() {
        return {productFields: [
        {key: 'name', label: 'Nimi'},
       {key:'category', label: 'Kategooria'}, 
       {key:'weight', label: 'Kaal(g)'},
    
        {key: 'kgprice', label:'KG hind'},
        {key:'price', label: 'Hind'},
        ],    
      productItems: [] ,

        }
    },
    async created () {
    const products = await axios({
      url: 'api/products',
      method: 'GET',
      headers: {}
    })
    console.log('products', products)
    this.productItems = products.data.allProducts
  },
    methods: {
  }
    }
</script>
<style scoped>
  h3 {
    margin: 40px 0 0;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #42b983;
  }
</style>