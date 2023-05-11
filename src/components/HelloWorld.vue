<template>
  <div>
    <input v-model="searchData" type="text" class="searchCss" placeholder="Search">
    <button @click="search()" class="searchCss buttonColor">Search</button>
  </div>
  <div class="">
      <table class="table" style="border:2px solid black">
        <thead>
            <tr>
                <th>Id</th>
                <th>title</th>
                <th :style="width=50">description</th>
                <th>price</th>
                <th>discountPercentage</th>
                <th>rating</th>
                <th>stock</th>
                <th>brand</th>
                <th>category</th>
                <th>thumbnail</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="product in products" :key="product.id">
                <td>{{product.id}}</td>
                <td>{{product.title}}</td>
                <td>{{product.description}}</td>
                <td>{{product.price}}</td>
                <td>{{product.discountPercentage}}</td>
                <td>{{product.rating}}</td>
                <td>{{product.stock}}</td>
                <td>{{product.brand}}</td>
                <td>{{product.category}}</td>
                <td><img :src="product.thumbnail" height="60" width="60" /></td>
            </tr>
        </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data: ()=>({
      products:null,
      searchData:'',
  }), 
  mounted() {
    fetch('https://dummyjson.com/products')
    .then(res => res.json())
    .then(json => this.products=json.products)
  },
  methods:{
      search(){
        fetch('https://dummyjson.com/products/search?q='+this.searchData)
        .then(res => res.json())
        .then(json => this.products=json.products);
      }

  }
}
</script>
<style scoped>


table, th, td {
  border-collapse: collapse;
  border: 1px solid;
  margin: 25px;
  padding: 10px;
}
.searchCss{
  float: left;
  line-height: 2;
  margin-left: 25px;
  margin-top: 20px;
  border-radius: 5px;
}
.buttonColor{
  background-color: #007bff;
  color: white;
}

</style>
