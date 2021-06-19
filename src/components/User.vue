<template>
  <div>
    <h1> Daftar User</h1>
    <ul>
    <li v-for="item in todos" :key="item.id">{{ item.desk}} <button @click="hapus(item.ID)">X</button></li>
    </ul>
    <input v-model="username"/>
    <input v-model="password"/>
    <button @click="tambah">Add</button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data: function (){
    return {
      users: [],
      username: '',
      password: ''
    }
  },
  created: function () {
    const username = localStorage.getItem('usr')
    const password = localStorage.getItem('pwd')
    axios.get('http://localhost:3000/user', { headers: {username, password}})
    .then(result => {
        this.todos = result.data  
    })
  },
  methods: {
    tambah: function () {
      const username = localStorage.getItem('usr')
      const password = localStorage.getItem('pwd')
      const item = {Deskripsi: this.myText}
      axios.post('http://localhost:3000/user', item, { headers: {username, password}})
      .then(() => {
        this.todos.push(item)
      })
    },
    hapus: function (id) {
      const username = localStorage.getItem('usr')
      const password = localStorage.getItem('pwd')
      axios.delete(`http://localhost:3000/user/${id}`, { headers: {username, password }})
    }
    }
}

</script>
