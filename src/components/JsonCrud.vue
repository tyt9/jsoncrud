<script>
import axios from "axios";

export default {
  data() {
    return {
      id:0,
      title: '',
      userId: 0,
      completed: false
    }
  },
  methods: {
    get: function () {
      let dataCollection = []
      axios.get('http://localhost:4000/todo')
        .then(res => {
          dataCollection = res.data
          console.log('dataCollection: ', dataCollection);
          dataCollection.forEach(data => {
            document.querySelector('.print-data').innerHTML
              += `<li>id: ${data.id} <br>title: ${data.title} <br> content: ${data.completed}</li>`
          })
        })
        .catch((error) => console.log(error))
    },
    submit: function () {
      const todoParams = {
        id: this.id,
        userId: this.userId,
        title: this.title,
        completed: this.completed
      }

      axios.post(`http://localhost:4000/todo`, todoParams)
        .then(res => {
          console.log('res: ', res);
        })
        .catch(error => {
          console.log('error: ', error);
        })
    },
    put: function () {
      const todoParams = {
        id: this.id,
        userId: this.userId,
        title: this.title,
        completed: this.completed
      }

      axios.put(`http://localhost:4000/todo/${this.id}`, todoParams)
        .then(res => {
          console.log('res: ', res);
        })
        .catch(error => {
          console.log('error: ', error);
        })
    },
    del: function () {
      axios.delete(`http://localhost:4000/todo/${this.id}`)
        .then(res => {
          console.log('res: ', res);
        })
        .catch(error => {
          console.log('error: ', error);
        })
    }
  }
}
</script>

<template>
<div id="app">
    <div class="box-wrap">
      <div class="box">아이디</div>
      <div class="box"><input v-model="id" placeholder="아이디를 입력"></div>
    </div>

    <div class="box-wrap">
      <div class="box">제목</div>
      <div class="box"><input v-model="title" placeholder="제목을 입력"></div>
    </div>

    <div class="box-wrap">
      <div class="box">사용자 아이디</div>
      <div class="box"><input v-model="userId" placeholder="사용자 아이디를 입력"></div>
    </div>

    <div class="box-wrap">
      <div class="box">성공여부</div>
      <div class="box"><input v-model="completed" placeholder="성공여부를 입력"></div>
    </div>

    <div class="box-wrap">
      <div class="box"><button class="button" v-on:click="get" type="button">GET</button></div>
      <div class="box"><button class="button" v-on:click="submit" type="button">POST</button></div>
      <div class="box"><button class="button" v-on:click="put" type="button">PUT</button></div>
      <div class="box"><button class="button" v-on:click="del" type="button">DELETE</button></div>
    </div>

    <div class="print-data">
      <ul></ul>
    </div>
</div>
</template>

<style>
.box-wrap {
  display: table;
  width: 100%;
  height: 30px;
  table-layout: fixed;
}

.box-wrap .box {
  display: table-cell;
  text-align: left;
  vertical-align: middle;
//border: 1px grey solid;
}
.button {
  width: 100%;
  height: 30px;
}
</style>
