<template>
    <div class="ExpensesListView">
        <transition-group name="list" tag="ul">
            <ExpensesPositionView
                v-for="post in posts"
                :key="post.id"
                :post="post"
                @deletePost="emitDeletePost"
                @editPost="emitEditPost"
            />
        </transition-group>
    </div>
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
.list-enter-active, .list-leave-active {
  transition: all .5s;
}
.list-enter, .list-leave-to {
  opacity: 0;
  transform: translateX(-50%);
}
</style>