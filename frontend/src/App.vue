<template>
  <div>
    <h1>Front end</h1>
    <fieldset>
      <legend>Cadastro</legend>
      <input type="text" v-model="tarefa.descricao" />
      <p>
        <button @click="salvar">Salvar</button>
      </p>
    </fieldset>
    <table>
      <thead>
        <tr>
          <th>Id</th>
          <th>Descrição</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(t, idx) in listatarefas" v-bind:key="idx">
          <td>{{ t.id }}</td>
          <td>{{ t.descricao }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      listatarefas: [],
      tarefa: {
        id: null,
        descricao: ''
      }
    }
  },
  mounted() {
    this.recuperar();
  },
  methods: {
    salvar() {
      fetch("http://localhost:8080/tarefas", {
        method: 'POST',
        body: JSON.stringify(this.tarefa),
        headers: {
          'Content-Type': 'application/json'
        }
      }).then(r => {
        console.log(r);
        this.recuperar();
      })
    },
    recuperar() {
      fetch("http://localhost:8080/tarefas", {
        method: 'GET'
      }).then(r => {
        return r.json();
      }).then(j => {
        console.log(j);
        this.listatarefas = j;
      })
    }
  }
}
</script>

<style>
table {
  width: 100%;
}

td {
  padding: 3px;
}
</style>
