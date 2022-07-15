<template>
  <div class="container">
    <h1>Todo App With Vue</h1>
    <hr />
    <div class="form-todo form-group">
      <input type="text" placeholder="nome" name="author" class="form-control" v-model="name">
      <textarea placeholder="Todo Message" name="author" class="form-control" v-model="message"></textarea>
      <button class="btn btn-primary" v-on:click="addTodo">Adicionar Todo</button>

      <div class="list-group" v-for="(comment, index) in setComments">
        <div class="list-group-item">
          <span class="comment__author">Author: <strong>{{comment.name}}</strong></span>
          <p>{{comment.message}}</p>

          <a href="#" class="comment__delete" v-on:click.prevent="deleteTodo(index)">Delete</a>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
  export default ({
    data() { //todos os dados da aplicação
      return {
        comments: [],
        name: '',
        message: ''
      }
    },
    methods: { //todas as funções da aplicação
      addTodo() {
        if(this.message.trim() === '') {
          return;
        }

        this.comments.push({
          name: this.name,
          message: this.message
        });
        this.name = '';
        this.message = '';
      },

      deleteTodo(index) {
        this.comments.splice(index, 1)
      },
    },
    computed: { //todas as funções visuais da aplicação, nada aqui é computado, apenas são chamadas
      setComments() {
        return this.comments.map(comment => ({
          ...comment,
          name: comment.name.trim() === '' ? "Anônimo" : comment.name
        }));
      }
    },
    watch: { //monitora a ação de qualquer dado
      comments(val) {
        console.log(val)
      }

    }
  })
</script>