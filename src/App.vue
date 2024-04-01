<script setup>
import { reactive, ref } from 'vue'

const titulo = ref("Meu VueJS!");
const mostrarResultado = ref(false)

const produto = reactive({
  nome: '',
  preco: 0,
  estoque: 0,
  categorias: []
})

const categorias=[
{
  id:1,
  nome:'JOIAS'
},
{
  id:2,
  nome:'ELETROLUX'
}]


function formatarPreco(preco) {
  try {
    return `R$ ${preco.toFixed(2).replace(".", ",")}`
  }
  catch (e) {
    return `Invalido`
  }
}

</script>

<template>
  <h1>{{ titulo }}</h1>
  <div class="container">
    <div class="formulario">
      <h2>Formulário</h2>
      <input type="text" v-model="titulo" />
      <hr />
      <div class="row">
        <label for="">Nome: </label>
        <input type="text" v-model="produto.nome">
      </div>
      <div class="row">
        <label for="">Preço: </label>
        <input type="number" v-model.number="produto.preco">
      </div>
      <div class="row">
        <label for="">Estoque: </label>
        <input type="number" v-model="produto.estoque">
      </div>
      <fieldset>
        <legend>Categorias:</legend>
        <div v-for="categoria in categorias" :key="categoria.id"><input type="checkbox" v-model="produto.categorias" :value= categoria.id /> {{categoria.nome}}</div>
      </fieldset>
      <button @click="mostrarResultado = !mostrarResultado">Mostrar resultado</button>
    </div>
    <Transition>
      <div v-if="mostrarResultado" class="resultado">
        <h2>Resultado</h2>
        <h3> Dados do produto</h3>
        <p>Nome: {{ produto.nome }}</p>
        <p>Preco: {{ formatarPreco(produto.preco) }}</p>
        <p>Estoque: {{ produto.estoque }}</p>
        <p>Categorias: {{ produto.categorias }}</p>
        <p> {{ mostrarResultado }}</p>
      </div>
    </Transition>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: row;
  column-gap: 1rem;
  margin-top: 1rem;
}

.resultado,
.formulario {
  min-height: 80vh;
  width: 48vw;
  border-radius: 30px;
  padding: 10px;
}

.formulario,
.formulario h2 {
  background-color: rgb(165, 250, 250);
}

.resultado,
.resultado h2 {
  background-color: aquamarine;
}

.row,
p,
h3 {
  background-color: rgb(117, 180, 159)
}

.v-enter-active,
.v-leave-active {
  transition: opacity 2s ease;
}

.v-enter-from {
  opacity: 0;
}

.v-enter-to {
  opacity: 1;
}
fieldset{
padding: 30px;
}
</style>
