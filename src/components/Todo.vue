<template>
  <div>
    <h1> Daftar Pekerjaan</h1>
    <ul>
    <li v-for="item in todos" :key="item.ID">{{ item.Deskripsi}} <button @click="hapus(item.ID)">X</button></li>
    </ul>
    <input v-model="myText"/>
    <button @click="tambah">Add</button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data: function (){
    return {
      todos: [],
      myText: ''
    }
  },
  created: function () {
    const username = localStorage.getItem('usr')
    const password = localStorage.getItem('pwd')
    axios.get('http://localhost:3000/todo', { headers: {username, password }})
    .then(result => {
      this.todos = result.data
    })
  },
  methods: {
    tambah: function () {
      const username = localStorage.getItem('usr')
      const password = localStorage.getItem('pwd')
      const item = {Deskripsi: this.myText}
      axios.post('http://localhost:3000/todo', item, { headers: {username, password}})
      .then(() => {
        this.todos.push(item)
      })
    },
    hapus: function (id) {
      const username = localStorage.getItem('usr')
      const password = localStorage.getItem('pwd')
      axios.delete(`http://localhost:3000/todo/${id}`, { headers: {username, password }})
    }
  }
}

</script>
