<template>
    <div class="app">
        <h1>Страница с постами</h1>
        <my-button
            @click="showDialog"
            style="margin: 15px 0;"
        >
            Создать пость
        </my-button>
        <my-dialog v-model:show="dialogVisible" >
            <post-form
                @create="createPost"
            />
        </my-dialog>

        <post-list 
            :posts="posts"
            @remove="removePost"
            v-if="!isPostsLoading"
        />
        <div v-else>Идет загрузка...</div>
    </div>
</template>

<script>
import PostForm from './conponents/PostForm.vue'
import PostList from './conponents/PostList.vue'
import PostItem from './conponents/PostItem.vue'
import axios from 'axios'
import MyButton from './conponents/UI/MyButton.vue'
export default {
    components: {
        PostForm, PostList, PostItem,
        MyButton
    },
    data() {
        return {
            posts: [],
            dialogVisible: false,
            isPostsLoading: false
        }
    },
    methods: {
        createPost(post) {
            this.posts.push(post);
            this.dialogVisible = false;
        },
        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id)
        },
        showDialog() {
            this.dialogVisible = true
        },
        async fetchPosts() {
            try {
                this.isPostsLoading = true;
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
                this.posts = response.data;
                console.log(response)
            } catch (e) {
                alert('Ошибка')
            } finally {
                this.isPostsLoading = false;
            }
        }
    },
    mounted() {
        this.fetchPosts();
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