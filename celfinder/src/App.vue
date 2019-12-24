<template>
  <div id="app">
    <div class="container">
      <div class="columns">
        <div class="column is-two-half">
          <h1 class="title has-text-dark">Abrir um novo chamado</h1>

          <div class="field">
            <label class="label">Titulo</label>
            <div class="control">
              <input v-model="title" class="input is-primary" type="text" placeholder="Titulo" />
            </div>
          </div>

          <div class="field">
            <label class="label">Cidade</label>
            <div class="control">
              <div class="select is-primary">
                <select v-model="city">
                  <option :key="item.id" v-for="item in cities">{{ item }}</option>
                </select>
              </div>
            </div>
          </div>

          <div class="field">
            <label class="label">Responsavel</label>
            <div class="control">
              <div class="select is-primary">
                <select v-model="responsible">
                  <option :key="item.id" v-for="item in responsibles">{{ item }}</option>
                </select>
              </div>
            </div>
          </div>

          <label class="label">Confirmar</label>
          <div class="field is-grouped">
            <div class="control">
              <button @click="addNote()" class="button is-link is-success">Adicionar</button>
            </div>
            <div class="control">
              <button class="button is-link is-danger">Cancelar</button>
            </div>
          </div>
        </div>

        <div class="column">
          <h1 class="title">Chamados em aberto</h1>
          <div class="container">
            <div class="card" :key="item.id" v-for="item in ticket">
              <header class="card-header has-background-dark">
                <p class="card-header-title has-text-white">{{ item.titulo }}</p>
                <a href="#" class="card-header-icon" aria-label="more options">
                  <span class="icon">
                    <i class="fas fa-angle-down" aria-hidden="true"></i>
                  </span>
                </a>
              </header>
              <div class="card-content">
                <div class="content">
                  <div class="sutitle"><strong>{{item.responsavel}} </strong></div>
                  
                    <div class="tag is-success">{{item.cidade}}</div>
                  

                  <br/>
                  <time datetime="2016-1-1">{{item.data}}</time>
                </div>
              </div>
              <footer class="card-footer">
                <a href="#" class="card-footer-item has-text-black">Concluido</a>
                <a href="#" class="card-footer-item has-text-black">Arquivar</a>
                <a href="#" class="card-footer-item has-text-black">Deletar</a>
              </footer>
            </div>
            <br />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
const axios = require("axios");

//axios.get("http://localhost:3000/service-order/find/all")
//let lista = []
//  .then(this.lista = response =>{
//
//    console.log(lista)
//});

export default {
  data() {
    return {
      ticket: [],
      title: "",
      city: "",
      responsible: "",
      responsibles: ["ALT", "FiberFort", "Daniel Fibra"],
      cities: ["Alumínio", "Cotia", "São Roque", "Itapevi", "Vargem Grande"],

    };

  },

  mounted() {
    axios
      .get("http://localhost:3000/service-order/find/all")
      .then(response => (this.ticket = response.data));
  },
  methods: {
    addNote() {
      axios
        .post("http://localhost:3000/service-order/insert", {
          body: this.ticket
        })
        .then(response => {})
        .catch(e => {
          this.errors.push(e);
        });

      console.log("Nova nota adicionada...");
      console.log(this.title);
      console.log(this.city);
      console.log(this.responsible);

      this.ticket.push({
        title: this.title,
        city: this.city,
        responsible: this.responsible
      });
      (this.title = ""), (this.city = ""), (this.responsible = "");
    },
    removeTicket() {
      console.log(index);
    }
  }
};
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 60px;
  margin-left: 30px;
  margin-right: 30px;
}
</style>
