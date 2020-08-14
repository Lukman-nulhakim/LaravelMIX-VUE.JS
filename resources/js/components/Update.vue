<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header text-center">Edit Buku</div>

                    <div class="card-body">
                        <form v-on:submit="submitPostEdit()">
                            <div class="form-group">
                                <input type="text" v-model="posts.title" class="form-control">
                            </div>
                            <div class="form-group">
                                <textarea v-model="posts.description" rows="5" class="form-control"></textarea>
                            </div>
                            <div class="form-group">
                                <router-link to="/" class="btn btn-warning">Kembali</router-link>
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

    created() {
        let id = this.$route.params.id;
        axios.get(`/posts/` + id + '/edit')
        .then(response => {
        // JSON responses are automatically parsed.
            this.posts = response.data
            })
            .catch(e => {
            this.errors.push(e)
            })
        },

  // ini script axios dari web alligator.io
    methods:{
        submitPostEdit() {
            let id = this.$route.params.id;
            axios.put(`/posts/` + id, this.posts) // this.posts ini manggil baris 33
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