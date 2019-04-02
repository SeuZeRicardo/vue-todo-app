<template>
  <div id="app">
    <div class="content ui three column grid">
      <div class="row">
        <div class="column">
          <div class="ui centered center">
            <p>Tarefas completas: {{showCompletedTasks}}</p>
            <p>Tarefas Pendentes: {{showPendingTasks}}</p>
          </div>
          <formTask v-on:add="newItem"/>
        </div>
        <div class="column">
          <!---
          O v-bind é o que passa para o componente os dados que estão locados nesse app,
          ele pega o valor do v-for com o valor de item
          -->
          <card v-for="item in todos" v-bind:item="item" v-on:delete="deleteTask"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

/* Exporta todos os componentes utitizados na aplicação */
import Card from './components/Card';
import FormTask from './components/FormTask';

export default {
  name: 'App',
  /* Define todos os componentes usados na aplicação */
  components: {
    Card,
    FormTask,
  },
  data() {
    return {
      todos: [{
        title: 'JS',
        project: 'Estudar sobre JS',
        done: true,
      }, {
        title: 'Vue',
        project: 'Estudar sobre Vue',
        done: true,
      }, {
        title: 'Praticar',
        project: 'Criar um Todo App',
        done: true,
      },
      ],
    };
  },
  /* Computed Property -> pega os dados e fazem uma logica mais complicada */
  computed: {
    showCompletedTasks() {
      let counter = 0;
      this.todos.filter(function ternary(item) {
        if (item.done === true) {
          counter += 1;
        }
        return this;
      });
      return counter;
    },
    showPendingTasks() {
      let counter = 0;
      this.todos.filter(function ternary(item) {
        if (item.done === false) {
          counter += 1;
        }
        return this;
      });
      return counter;
    },
  },
  /* Metodos -> Tem como objetivo executar um comando especifico */
  methods: {
    /* Adiciona uma nova tarefa no Array das demandas */
    newItem(task) {
      this.todos.push(task);
    },
    /* Deleta uma tarefa no Array das demandas */
    deleteTask(itemTask) {
      this.todos = this.todos.filter(item => item !== itemTask);
    },
  },
};
</script>

<style>
#app {
  padding: 20px;
}
</style>
