<template>
  <div id="app">
    <img id="logo" alt="Vue logo" src="./assets/logo.png">

    <h1>Vue Advices</h1>

    <div id="search-field">
      <input type="text" v-model="term" />
      <button v-on:click="search" >Search!</button>
    </div>

    <img id="loading" v-if="loading" src="./assets/loading.gif" alt="Loading">

    <ul>
      <li v-for="item in items" v-bind:key="item.slip_id">
        {{ item.advice }}
      </li>
    </ul>

  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'app',
    data() {
      return {
        term: '',
        items: [],
        loading: false,
      };
    },
    methods: {
      search() {
        this.items = [];
        this.loading = true;
        axios.get(`https://api.adviceslip.com/advice/search/${this.term}`).then(response => {
          this.loading = false;
          this.items = response.data.slips;
        })
      },
    },
  };
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  #logo {
    max-height: 100px;
  }

  #search-field {
    margin-bottom: 50px;
  }

  #search-field input {
    border: 1px solid grey;
    border-top-left-radius: 4px;
    border-bottom-left-radius: 4px;
    border-right: none;
    padding: 5px;
  }

  #search-field button {
    border: 1px solid grey;
    background: whitesmoke;
    border-top-right-radius: 4px;
    border-bottom-right-radius: 4px;
    padding: 5px;
  }

  #loading {
    width: 100%;
    max-width: 320px;
  }

  ul {
    list-style-type: none;
    padding: 0 15px;
    text-align: center;
  }

  ul li:not(:last-child) {
    margin-bottom: 30px;
  }
</style>
