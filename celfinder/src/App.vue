<template>
  <div id="app">
    <div class="container">
      <div class="columns">
        <div class="column">
          <div class="field">
            <label class="label">Novo chamado</label>
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
              <button @click="addNote" class="button is-link is-success">Adicionar</button>
            </div>
            <div class="control">
              <button class="button is-link is-danger">Cancelar</button>
            </div>
          </div>
        </div>

        <div class="column">
         <div>
           <section class="hero is-primary" :key="item.id" v-for="item in ticket">
            <div class="hero-body">
              <div class="container">
                
                <h1 class="title">{{ item.titulo}}</h1>

                <span class="tag is-warning">{{item.cidade}}</span>

                <h2 class="subtitle">{{item.responsavel}}</h2>

                <a href="#" @click="removeTicket(index)">Excluir</a>
              </div>
            </div>
          </section>
        


         </div>
          <!--<section class="hero is-primary" :key="item.id" v-for="(item, index) in ticket">
            <div class="hero-body">
              <div class="container">
                
                <h1 class="title">{{ item.title }}</h1>

                <span class="tag is-warning">{{ item.city}}</span>

                <h2 class="subtitle">{{item.responsible}}</h2>

                <a href="#" @click="removeTicket(index)">Excluir</a>
              </div>
            </div>
          </section>-->
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
  
  mounted () {
    axios
      .get('http://localhost:3000/service-order/find/all')
      .then(response => (this.ticket = response.data))},

  methods: {
    addNote() {
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
}
</style>
