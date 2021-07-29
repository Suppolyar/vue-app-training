<template>
    <div class="app">
        <post-form
            @create="createPost"
        />
        <post-list 
            :posts="posts"
        />        
    </div>
</template>

<script>
import PostForm from './conponents/PostForm.vue'
import PostList from './conponents/PostList.vue'
import PostItem from './conponents/PostItem.vue'
export default {
    components: {
        PostForm, PostList, PostItem
    },
    data() {
        return {
            posts: [
                {id: 1, title: 'JavaScript', body: 'Описание'},
                {id: 2, title: 'JavaScript 2', body: 'Описание 2'},
                {id: 3, title: 'JavaScript 3', body: 'Описание 3'}
            ],
        }
    },
    methods: {
        createPost(post) {
            this.posts.push(post);
        },
    }
}
</script>

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }
</style>