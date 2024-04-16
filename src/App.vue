<script setup>
import { ref } from 'vue'

const user = ref({
  name: '',
  lastName: '',
  email: '',
  dataNasc: '',
  city: '',
  state: '',
  hobbies: [],
  langProg: '',
  biography: ''
})

const userPass = ref({
  senha: '',
  confSenha: ''
})

const states = [
  { uf: 'AC', name: 'Acre' },
  { uf: 'AL', name: 'Alagoas' },
  { uf: 'AP', name: 'Amapá' },
  { uf: 'AM', name: 'Amazonas' },
  { uf: 'BA', name: 'Bahia' },
  { uf: 'CE', name: 'Ceará' },
  { uf: 'DF', name: 'Distrito Federal' },
  { uf: 'ES', name: 'Espírito Santo' },
  { uf: 'GO', name: 'Goiás' },
  { uf: 'MA', name: 'Maranhão' },
  { uf: 'MT', name: 'Mato Grosso' },
  { uf: 'MS', name: 'Mato Grosso do Sul' },
  { uf: 'MG', name: 'Minas Gerais' },
  { uf: 'PA', name: 'Pará' },
  { uf: 'PB', name: 'Paraíba' },
  { uf: 'PR', name: 'Paraná' },
  { uf: 'PE', name: 'Pernambuco' },
  { uf: 'PI', name: 'Piauí' },
  { uf: 'RJ', name: 'Rio de Janeiro' },
  { uf: 'RN', name: 'Rio Grande do Norte' },
  { uf: 'RS', name: 'Rio Grande do Sul' },
  { uf: 'RO', name: 'Rondônia' },
  { uf: 'RR', name: 'Roraima' },
  { uf: 'SC', name: 'Santa Catarina' },
  { uf: 'SP', name: 'São Paulo' },
  { uf: 'SE', name: 'Sergipe' },
  { uf: 'TO', name: 'Tocantins' }
]

const mostrarResultado = ref(false)

function salvarPerfil() {
  if (userPass.value.senha == userPass.value.confSenha) {
    mostrarResultado.value = true
  } else {
    alert('!!Senha incorreta!! \n!!Verifique!!')
  }
}
</script>

<template>
  <main>
    <h1>Editor de Perfil</h1>
    <transition name="form" mode="out-in">
      <div v-if="mostrarResultado" class="perfil">
        <p v-for="(value, key) of user" :key="key">{{ key }}: {{ value }}</p>

        <button type="submit" @click="mostrarResultado = false">Voltar</button>
      </div>
      <div v-else class="editPerfil">
        <form @submit.prevent="salvarPerfil()" validate>
          <div class="container-col3">
            <div class="col-3">
              <label for="">Nome: </label>
              <input type="text" v-model="user.name" minlength="3" required />
            </div>

            <div class="col-3">
              <label for="">Sobrenome: </label>
              <input type="text" v-model="user.lastName" minlength="3" required />
            </div>
            <div class="col-3">
              <label for="">Email: </label>
              <input type="email" v-model="user.email" required />
            </div>
          </div>
          <div class="container-col5">
            <div class="col-5">
              <label for="">Cidade: </label>
              <input type="text" v-model="user.city" />
            </div>
            <div class="col-5">
              <label for="">Estado: </label>
              <select v-model="user.state">
                <option selected disabled value="">Selecionar...</option>
                <option v-for="state of states" :key="state.uf" :value="state.uf">
                  {{ state.name }}
                </option>
              </select>
            </div>
            <div class="col-5">
              <label for="">Data de Nascimento: </label>
              <input type="date" v-model="user.dataNasc" />
            </div>
            <div class="col-5">
              <label for="">Senha: </label>
              <input type="password" v-model="userPass.senha" required />
            </div>

            <div class="col-5">
              <label for="">Confirme a senha: </label>
              <input type="password" v-model="userPass.confSenha" required />
            </div>
          </div>

          <div class="container-col2">
            <div class="hobbies col-2">
              <p>Hobbies:</p>

              <input type="checkbox" value="esportes" v-model="user.hobbies" />
              <label>Esportes</label>

              <input type="checkbox" value="musica" v-model="user.hobbies" />
              <label>Musicas</label>

              <input type="checkbox" value="viagem" v-model="user.hobbies" />
              <label>Viajar</label>

              <input type="checkbox" value="leitura" v-model="user.hobbies" />
              <label>Leitura</label>
            </div>
            <div class="langProg col-2">
              <p>Linguagem preferida:</p>
              <input type="radio" v-model="user.langProg" value="C" id="langC" />
              <label for="langC">C</label>
              <input type="radio" v-model="user.langProg" value="Java" id="langJava" />
              <label for="langJava">Java</label>
              <input type="radio" v-model="user.langProg" value="Python" id="langPython" />
              <label for="langPython">Python</label>
              <input type="radio" v-model="user.langProg" id="langJs" />
              <label for="langJs">JavaScript</label>
            </div>
          </div>
          <div class="container-col1">
            <div class="col-1">
              <h3 class="textCenter">Biografia</h3>
              <textarea name="Biography" id="Biography" v-model="user.biography"></textarea>
            </div>
          </div>

          <button type="submit">Verificar</button>
        </form>
      </div>
    </transition>
  </main>
</template>

<style scoped>
.form-enter-active,
.form-leave-active {
  transition: opacity 0.5s ease;
}

.form-enter-from,
.form-leave-to {
  opacity: 0;
}
label {
  display: inline-block;
  color: #977070;
}
input,
select {
  margin-right: 3rem;
  background-color: #1e263a;
  color: #97fecc;
}
.options:hover {
  transition-delay: 100ms;
  transition-duration: 500ms;
  transition-timing-function: linear;
  background-color: #8f866f;
  color: #0e3e27;
}

div {
  text-align: left;
}

.container-col1 {
  display: grid;
  grid-template-columns: auto;
}
.col-1 {
  grid-column: auto;
}
.col-1 textarea {
  display: flex;
  margin-right: auto;
  margin-left: auto;
  background-color: #b159ff;
  color: #fff45c;
  box-shadow: 2px 2px 1px #bc8f8f;
  border-radius: 7px;
}

.container-col2 {
  display: grid;
  grid-template-columns: auto auto;
  grid-template-rows: 1fr;
}
.col-2 {
  margin: 10px 10px 10px 0;
}
.langProg input,
.hobbies input {
  margin: 0 5px 0 15px;
}

.container-col3 {
  display: grid;
  grid-template-columns: auto auto auto;
}
.col-3 {
  display: flex;
  flex-direction: column;
  margin: 10px;
  flex: 0 0 auto;
}

.container-col5 {
  display: grid;
  grid-template-columns: auto auto auto auto auto;
}
.col-5 {
  display: flex;
  flex-direction: column;
  margin: 10px;
}
.textCenter {
  text-align: center;
  font-weight: bolder;
  font-style: italic;
  margin: 10px;
}

button {
  margin: 2rem;
  padding: 1rem;

  transition-delay: 100ms;
  transition-duration: 400ms;
  transition-timing-function: linear;
  background-color: #707990;
  color: #5f213f;
  box-shadow: 2px 2px 2px #343434;
  border: 2px solid #3f3f3f;
}
button:hover {
  transition-delay: 100ms;
  transition-duration: 400ms;
  transition-timing-function: linear;
  background-color: #8f866f;
  color: #0e3e27;
}
.perfil p {
  padding: 4px;
  color: #afafaf;
}

@media (max-width: 900px) {
  .container-col2,
  .container-col3,
  .container-col5 {
    grid-template-columns: auto auto;
  }
}
@media (max-width: 600px) {
  .container-col1,
  .container-col2,
  .container-col3,
  .container-col5 {
    grid-template-columns: auto;
  }
}
</style>
