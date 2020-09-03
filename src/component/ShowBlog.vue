<template>
    <div id="show-blogs">
        <h1>All Blog Articles</h1>
        <input type="text" v-model="search" placeholder="search blogs" />
        <div v-for="blog in filteredBlogs" class="single-blog" :key="blog">
            <router-link v-bind:to="'/blog/' + blog.id"><h2>{{ blog.title }}</h2></router-link>
            <article>{{ blog.body }}</article>
        </div>
    </div>
</template>

<script>
// Imports
import searchMixins from '../Mixins/searchMixins';
export default {
    data () {
        return {
            blogs: [],
            search: ''
        }
    },
    created() {
        this.$http.get('https://vue-test-26cba.firebaseio.com/posts.json').then(function(data){
            return data.json()
        }).then(function(data){
            var blogsArray = [];
            for (let key in data){
                data[key].id = key;
                blogsArray.push(data[key]);
            }
            this.blogs = blogsArray;
            //console.log(this.blogs);
        });
    },
    mixins: [searchMixins]
}
</script>

<style>
#show-blogs{
    max-width: 800px;
    margin: 70px auto;
}
.single-blog{
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;
}
#show-blogs a{
    color: #444;
    text-decoration: none;
}
</style>