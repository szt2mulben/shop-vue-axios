<template>
    <h1>Vasvári Boltja</h1>
    <div class="card-container">
      <div class="card" v-for="product in products" :key="product.id">
        <img src="../assets/no-image.png">
        <div class="card-content">
          <h3>Név: {{ product.name }}</h3><br>
          <p>Ár: {{ product.price }}</p><br>
          <button class="button" @click="">Részletek</button>
          <button class="button" @click="addToCart(product)">Kosárba</button>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import axios from 'axios';
  import { ref, onMounted } from 'vue';
  const products = ref([]);
  
  onMounted(() => {
    axios.get('http://localhost:3000/products')
      .then(resp => products.value = resp.data);
  });

  const addToCart = (product) => {
    let tombMerete = products.value.length;
    let id = Number(products.value[tombMerete - 1].id);
    let d = {id: product.id , name : product.name, price: product.price};
    console.log(d);    
    fetch("http://localhost:3000/cart",
    {
      method : 'post',
      body : JSON.stringify(d),
      headers : {
        "Content-type" : "application/json"
      }
    })
  }
 
  </script>
  
  <style scoped>
  h1{
    text-align: center;
    padding: 20px;
    font-family: fantasy ;

  }
  .card-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }
  
  .card {
    flex-basis: calc(25% - 20px);
    max-width: calc(25% - 20px);
    margin: 10px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    overflow: hidden;
    padding: 10px;
    background-color: #1f7e1f;
  }
  
  .card img {
    width: 100%;
    height: auto;
    border-radius: 10px 10px 0 0;
  }
  
  .card-content {
    padding: 20px;
    text-align: center;
  }
  
  .card-content h3 {
    margin-top: 0;
  }
  
  .button {
  display: inline-block;
  padding: 8px 16px;
  background-color: #006400;
  color: white;
  text-decoration: none;
  border-radius: 8px;
}
  @media (max-width: 768px) {
    .card {
      flex-basis: calc(50% - 20px);
      max-width: calc(50% - 20px);
    }
  }
  </style>
  