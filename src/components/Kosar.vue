<script setup>
  import { onMounted, ref  } from 'vue';
  const names = ref();

  const letoltes = () => {
    fetch('http://localhost:3000/cart')
    .then(resp => resp.json())
    .then(json => {
      names.value = json;
      console.log(names.value);
    })
  }

  onMounted(() => {
    letoltes();
  })

  const del = (id) =>{
    console.log(id)
    fetch("http://localhost:3000/cart/" + id,{
      method : "delete",
    })
    .then(() => letoltes())
  }
  
</script>

<template>
<h1>Kosárban lévő termékek</h1>
  <table>
    <tr v-for="n in names" key="n.id">
      <td> {{ n.name }}</td>
      <td> {{ n.price }}</td>
      <td> <span @click="del(n.id)">❌</span> </td>
    </tr>
    <button class="" @click="">Rendelés</button>

  </table>
</template>

<style scoped>
  table,td{
    border-collapse: collapse;
    text-align: center;
  }
  span:hover{
    cursor: pointer;
  }
  h1{
    text-align: center;
    padding: 20px;
    font-family: fantasy ;
  }

</style>