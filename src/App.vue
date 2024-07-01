<script setup>
import { reactive, ref } from 'vue'

const titulo = 'Edição de perfil';
const mostrarResultado = ref(false)

const info = reactive({
  nome: '',
  email: '@',
  senha: 0,
  confisenha: 0,
  datanascimento: 0,
  endereco: '',
  cidade: '',
  estado: [],
  hobbies: '',
  linguagemprog: [],
  biografia: ''
})

const estados = [
  {
    sigla: 'AC',
    nome: 'Acre'
  },
  {
    sigla: 'AL',
    nome: 'Alagoas'
  },
  {
    sigla: 'AP',
    nome: 'Amapá'
  },
  {
    sigla: 'AM',
    nome: 'Amazonas'
  },
  {
    sigla: 'BA',
    nome: 'Bahia'
  },
  {
    sigla: 'CE',
    nome: 'Ceará'
  },
  {
    sigla: 'DF',
    nome: 'Distrito Federal'
  },
  {
    sigla: 'ES',
    nome: 'Espírito Santo'
  },
  {
    sigla: 'GO',
    nome: 'Goiás'
  },
  {
    sigla: 'MA',
    nome: 'Maranhão'
  },
  {
    sigla: 'MT',
    nome: 'Mato Grosso'
  },
  {
    sigla: 'MG',
    nome: 'Minas Gerais'
  },
  {
    sigla: 'PA',
    nome: 'Pará'
  },
  {
    sigla: 'PB',
    nome: 'Paraíba'
  },
  {
    sigla: 'PR',
    nome: 'Paraná'
  },
  {
    sigla: 'PE',
    nome: 'Pernambuco'
  },
  {
    sigla: 'PI',
    nome: 'Piuaí'
  },
  {
    sigla: 'RJ',
    nome: 'Rio de Janeiro'
  },
  {
    sigla: 'RN',
    nome: 'Rio Grande do Norte'
  },
  {
    sigla: 'RS',
    nome: 'Rio Grande do Sul'
  },
  {
    sigla: 'RO',
    nome: 'Rondônia'
  },
  {
    sigla: 'RR',
    nome: 'Roraima'
  },
  {
    sigla: 'SC',
    nome: 'Santa Catarina'
  },
  {
    sigla: 'SP',
    nome: 'São Paulo'
  },
  {
    sigla: 'SE',
    nome: 'Sergipe'
  },
  {
    sigla: 'TO',
    nome: 'Tocantins'
  },
]
const linguagensprog = [
  {
    nome: 'Python'
  },
  {
    nome: 'JavaScript'
  },
  {
    nome: 'C++'
  },
  {
    nome: 'Java'
  },
  {
    nome: 'PHP'
  }
]

function processarForm() {
  if ((info.senha == info.confisenha) && info.email.includes("@")) {
    mostrarResultado.value = !mostrarResultado.value
  }
}

function formatarNome(nome) {
  console.log(info.nome)
  if (info.nome == "") {
    return 'O campo não foi preenchido'
  }
  return info.nome
}

function formatarData(datanascimento) {
  if (info.datanascimento == 0) {
    return 'O campo não foi preenchido'
  }
  return info.datanascimento
}

function formatarSenha(senha) {
  console.log(info.senha)
  if (Array.from(info.senha).length < 4) {
    return 'A senha precisa ter no mínimo 4 caracteres'
  }
  return info.senha
}

function formatarEndereco(endereco) {
  if (info.endereco == "") {
    return 'O campo não foi preenchido'
  }
  return info.endereco
}

function formatarHobbies(hobbies) {
  if (info.hobbies == "") {
    return 'O campo não foi preenchido'
  }
  return info.hobbies
}

function formatarBio(biografia) {
  if (info.biografia == "") {
    return 'O campo não foi preenchido'
  }
  return info.biografia
}

function formatarCidade(cidade) {
  if (info.cidade == "") {
    return 'O campo não foi preenchido'
  }
  return info.cidade
}

</script>

<template>
  <h1>{{ titulo }}</h1>
  <div class="container">
    <div class="formulario">
      <h2>Formulário</h2>
      <hr />
      <div class="row">
        <label for="">Nome: </label>
        <input type="text" v-model="info.nome" required>
      </div>
      <div class="row">
        <label for="">E-mail: </label>
        <input type="text" v-model.number="info.email">
      </div>
      <div class="row">
        <label for="">Senha: </label>
        <input type="number" v-model="info.senha">
      </div>
      <div class="row">
        <label for="">Confirmar Senha: </label>
        <input type="number" v-model="info.confisenha">
      </div>
      <div class="row">
        <label for="">Data de Nascimento: </label>
        <input type="date" v-model="info.datanascimento">
      </div>
      <div class="row">
        <label for="">Endereco: </label>
        <input type="text" v-model="info.endereco">
      </div>
      <div class="row">
        <label for="">Cidade: </label>
        <input type="text" v-model="info.cidade">
      </div>
      <div class="row">
        <label for="info.estado">Estado:</label>
        <select v-model="info.estado">
          <option v-for="estado in estados" :key="estado.sigla" :value="estado.nome">({{ estado.sigla }})
            {{ estado.nome }} </option>
        </select>
      </div>
      <div class="row">
        <label for="">Hobbies: </label>
        <input type="text" v-model="info.hobbies">
      </div>
      <fieldset>
        <legend>Linguagem de programação: </legend>
        <template v-for="linguagem in linguagensprog" :key="linguagem.nome">
          <input v-model="info.linguagemprog" :value="linguagem.nome" type="checkbox">
          {{ linguagem.nome }}
        </template>
      </fieldset>
      <div class="row">
        <label for="">Biografia: </label>
        <input type="text" v-model="info.biografia">
      </div>
      <button @click="processarForm">Mostrar resultado</button>
    </div>
    <!-- <Transition> -->
    <!-- <template> -->

    <div v-if="mostrarResultado" class="resultado">
      <h3>Perfil</h3>
      <p>Nome: {{ formatarNome(info.nome) }}</p>
      <p>E-mail: {{ info.email }}</p>
      <p>Senha: {{ formatarSenha(info.senha) }}</p>
      <p>Data de Nascimento: {{ formatarData(info.datanascimento) }}</p>
      <p>Endereço: {{ formatarEndereco(info.endereco)}}</p>
      <p>Cidade: {{ formatarCidade(info.cidade) }}</p>
      <p>Estado: {{ info.estado }}</p>
      <p>Hobbies: {{ formatarHobbies(info.hobbies) }}</p>
      <p>Linguagens de programação: {{ info.linguagemprog }}</p>
      <p>Biografia: {{ formatarBio(info.biografia) }}</p>
    </div>
    <div v-if="info.confisenha != info.senha">
      <p>O campo de confirmação de senha não corresponde ao campo senha.</p>
    </div>
    <div v-if="!info.email">
      <p>O e-mail informado não é válido</p>
    </div>
    <!-- </template>
    </Transition> -->
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
  background-color: rgba(253, 253, 253, 0.514);
}

.resultado,
.resultado h2 {
  background-color: rgba(253, 253, 253, 0.514);
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

fieldset {
  padding: 30px;
}
</style>
