<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header text-center">Lihat Buku</div>
                    <div class="card-body">
                        <form v-on:submit="submitPost()">
                            <div class="form-group">
                                <input type="text" v-model="posts.title" placeholder="Masukan Judul" class="form-control">
                            </div>
                            <div class="form-group">
                                <textarea v-model="posts.description" rows="5" placeholder="Masukan Deskripsi" class="form-control"></textarea>
                            </div>
                            <div class="form-group">
                                <router-link to="/" class="btn btn-warning">Tambah Buku</router-link>
                                <button class="btn btn-success">Simpan</button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data:function() {
    return {
    posts: { // ini manggil migrations
            title:"",
            description:""
    },
        errors: []
    }
},

  // ini script axios dari web alligator.io
    methods:{
        submitPost() {
            axios.post(`/posts`, this.posts) // this.posts ini manggil baris 33
            .then(response => { // pas di simpan ada respone console, balik lagi / , dan menyimpan datanya
                console.log(response)
                this.$router.push({path:'/'})
                this.posts = response.data 
            })
            .catch(e => {
            this.errors.push(e)
            })
        }
    }
}
</script>
