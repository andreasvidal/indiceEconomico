<template>
  <div class="container">
    <div class="row">
      <div class="col-lg">
        <h1 class="text-center m-4" >Variación </h1>
      </div>
    </div>
    <!--acá recibo código y filtro la información segun valor financiero y 
     muestro una lista con valor y fecha https://mindicador.cl/api/{tipo_indicador} // 
     mostral listado donde pararezca todo lo de la url {{$route.params.valor}}-->
    <div class="row d-flex">
      <div class="col-lg-4" v-for="item in arrayData" :key="item">
        <div class="card m-2">
          <span class="span mx-auto"> {{ name }}</span>
        <strong class="mx-auto rounded">$ {{ formatPrice(item.valor) }}</strong>
        <span class="span mx-auto">Fecha {{ formatDate(item.fecha) }}</span>
        </div>
      </div>
    </div>
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
      data: "",
      name: "",
      arrayData: [],
    };
  },
  created() {
    const data = this.$route.params.valor;  
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

    console.log(data);
    axios.get(`https://mindicador.cl/api/${data}`).then((result) => {
      console.log(result.data);
      this.arrayData = result.data.serie;
      this.name = result.data.nombre;
      console.log(name)
    });
  },
  methods: {
    formatPrice(value) {
      let val = (value / 1).toFixed(0).replace(".", ",");
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
    },
    formatDate(date) {
      var d = new Date(date),
        month = '' + (d.getMonth() + 1),
        day = '' + d.getDate(),
        year = d.getFullYear();

      if (month.length < 2) 
        month = '0' + month;
      if (day.length < 2) 
        day = '0' + day;

      return [day , month, year].join('-');
    }, 
  },
};
</script>

<style>
.container{
  align-items: center;
  background-color: rgba(0, 0, 0, 0.274);
  width: 90%;
  margin-top: 1rem;
}
.list{
  list-style:none;
}

.list-group-item{
  background-color: #c5c5c5;
  margin: 1rem;
  padding: 0.5rem 2rem;
}

.span{
  margin: 0 0.5rem;
}

</style>
