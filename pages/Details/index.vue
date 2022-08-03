<template>
  <div>
    <h2>{{ title }}</h2>
    <!--funcion creada en methos para settear el valor de la uf a formato pesos-->
    <ul>
      <li><a :href="'/Details/'+ uf.codigo">{{uf.nombre}}</a></li>
      <li><a :href="'/Details/'+ utm.codigo">{{utm.nombre}}</a></li>
      <li><a :href="'/Details/'+ dolar.codigo">{{dolar.nombre}}</a></li>
      <li><a :href="'/Details/'+ euro.codigo">{{euro.nombre}}</a></li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      uf: [],
      utm: [],
      dolar: [],
      euro: [],
    };
  },
  created() {

    const data = this.limit;
    console.log(data);
    axios.get(`https://mindicador.cl/api`).then((result) => {
      console.log(result.data);
      this.uf = result.data.uf;
      this.utm = result.data.utm;
      this.dolar = result.data.dolar;
      this.euro = result.data.euro;
    });
  },
  methods: {
    formatPrice(value) {
      let val = (value / 1).toFixed(0).replace(".", ",");
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
    },
    
  },
};
</script>

<style></style>
