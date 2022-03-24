<template>
    <ul class="ExpensesListView">
        <ExpensesPositionView
            v-for="post in posts"
            :key="post.id"
            :post="post"
            @deletePost="emitDeletePost"
            @editPost="emitEditPost"
        />
    </ul>
</template>

<script>
import ExpensesPositionView from "./ExpensesPositionView.vue";

export default {
    name: "ExpensesListView",
    components: {
        ExpensesPositionView,
    },
    props: {
        posts: {
            type: Array,
            default: [],
        },
    },
    methods: {
        emitDeletePost(id) {
            this.$emit("deletePost", id);
        },
        emitEditPost(editablePost) {
            this.$emit("editPost", editablePost);
        },
    },
};
</script>

<style scoped>
</style>