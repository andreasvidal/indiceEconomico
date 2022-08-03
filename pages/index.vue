<template>
  <div class="container">
    <h1 class="text-md-center text-secondary pb-3 pt-3">Indicadores Económicos</h1>
    <div class="row d-flex">
    <div class="row row-cols-auto m-4">
      <DisplayCard class="col m-1 text-center m-2 bg-secondary rounded" limit="uf"></DisplayCard>
      <DisplayCard class="col m-1 text-center m-2 bg-secondary rounded" limit="utm"></DisplayCard>
      <DisplayCard class="col m-1 text-center m-2 bg-secondary rounded" limit="dolar"></DisplayCard>
      <DisplayCard class="col m-1 text-center m-2 bg-secondary rounded" limit="euro"></DisplayCard>
    </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "IndexPage",
};
</script>

<style>
.container{
  align-items: center;
  background-color: rgba(0, 0, 0, 0.274);
  width: 90%;
  margin-top: 1rem;
}</style>