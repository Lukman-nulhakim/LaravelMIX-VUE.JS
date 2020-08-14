<template>
    <div class="card">
        <div class="card-header">
            <router-link to="/create" class="btn btn-primary">Tambah Buku</router-link>
        </div>

        <div class="card-body">
            <table class="table table-hover">
                <thead>
                    <tr>
                        <th scope="col">Title</th>
                        <th scope="col">Deskripsi</th>
                        <th width="100"></th>
                        <th width="100"></th>
                        <th width="100"></th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="post, index of posts">
                        <th>{{ post.title }}</th>
                        <th>{{ post.description }}</th>
                        <td>
                            <router-link :to="{ name: 'readPost', params:{id:post.id}}" class="btn btn-primary">Lihat</router-link>
                        </td>
                        <td><router-link :to="{name: 'editPost', params:{id:post.id}}" class="btn btn-success">Edit</router-link></td>
                        <td><button class="btn btn-danger" v-on:click="submitPostDelete(post.id,index)">Hapus</button></td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      posts: [],
      errors: []
    }
  },

  // Fetches posts when the component is created.
  created() {
    axios.get(`/posts`)
    .then(response => {
      // JSON responses are automatically parsed.
      this.posts = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  },

  // ini method buat delete
    methods:{
      submitPostDelete(id, index) {
        if (confirm("Apakah anda ingin menghapus data ini ?")) {
          axios.delete(`/posts/` + id, this.posts) // this.posts ini manggil baris 33
          .then(response => { // pas di simpan ada respone console, balik lagi / , dan menyimpan datanya
              console.log(response)
              this.posts.splice(index, 1)
          })
          .catch(e => {
          this.errors.push(e)
          })
        }
      }
    }
}
</script>