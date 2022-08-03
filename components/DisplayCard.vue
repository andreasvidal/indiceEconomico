<template>
  <div>
    <h2 class="m-2 text-size">{{ title }}<hr></h2>
    <!--funcion creada en methos para settear el valor de la uf a formato pesos-->
    <h4 class="m-2">$ {{ formatPrice(value) }}</h4>
    <span>Fecha {{ date }}</span>
    <a class=" mt-4 mb-4 btn btn-info" :href="'/Details/'+ limit"><i class="bi bi-search mr-2"></i>Ver detalles</a> 
  </div>
  
</template>

<script>
import axios from "axios";
export default {
  props: {
    limit: {
      type: String,
    },
    dateToday: {
      type: String,
    },
  },
  data() {
    return {
      title: "",
      value: 0,
      date: "",
    };
  },
  created() {
    const date = new Date();
    let year = date.getFullYear();
    let month = date.getMonth() + 1;
    let dt = date.getDate();

    if (dt < 10) {
      dt = "0" + dt;
    }
    if (month < 10) {
      month = "0" + month;
    }
    const dateToday = dt + "-" + month + "-" + year;
    const data = this.limit;
    console.log(data);
    axios
      .get(`https://mindicador.cl/api/${data}/${dateToday}`)
      .then((result) => {
        console.log(result.data);
        this.title = result.data.nombre
        this.value = result.data.serie[0].valor
        this.date = dateToday
      });
  },
  methods:{
     formatPrice(value) {
            let val = (value / 1).toFixed(0).replace(".", ",");
            return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
        },
  }
};
</script>

<style>
.text-size{
    font-size: 1.5rem;
}
</style>
