<template>
    <li class="ExpensesPositionView">
        <div class="ExpensesPositionView__text-wrapper" v-show="!isChanging">
            <p class="ExpensesPositionView__name">{{ this.post.name }}</p>
            <p class="ExpensesPositionView__coast">-{{ this.post.sum }}₽</p>
        </div>
        <div class="ExpensesCreateView__text-wrapper" v-show="isChanging">
            <input
                v-model="newName"
                class="ExpensesCreateView__name"
                :placeholder="this.post.name"
            />
            <input
                v-model="newValue"
                class="ExpensesCreateView__coast"
                :placeholder="this.post.sum"
                type="number"
            />
        </div>
        <div class="ExpensesPositionView__btn-wrapper">
            <ExpensesEditButton :postId="post.id" @editPost="emitEditPost" />
            <ExpensesDeleteButton
                v-show="!isChanging"
                :postId="post.id"
                @deletePost="emitDeletePost"
            />
            <ExpensesCancelButton v-show="isChanging" @click="cancelEdit" />
        </div>
    </li>
</template>

<script>
import ExpensesEditButton from "./ExpensesEditButton.vue";
import ExpensesDeleteButton from "./ExpensesDeleteButton.vue";
import ExpensesCancelButton from "./ExpensesCancelButton.vue";

export default {
    name: "ExpensesPositionView",
    components: {
        ExpensesEditButton,
        ExpensesDeleteButton,
        ExpensesCancelButton,
    },
    props: {
        post: {
            type: Object,
            default: {},
        },
    },
    data: () => ({
        isChanging: false,
        newName: "",
        newValue: 0,
    }),
    methods: {
        emitDeletePost(id) {
            this.$emit("deletePost", id);
        },
        emitEditPost() {
            if (this.isChanging) {                
                const editablePost = {
                    name: this.newName || this.post.name,
                    sum: this.newValue,
                    id: this.post.id
                }
                
                this.isChanging = false;
                this.$emit("editPost", editablePost);
            } else {
                this.isChanging = true;
            }
        },
        cancelEdit() {
            this.isChanging = false;
        },
    },
};
</script>

<style scoped>
li.ExpensesPositionView {
    padding: 3vw;

    display: flex;
    justify-content: space-between;
    align-items: center;
}
.ExpensesPositionView__text-wrapper {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: center;

    width: 60vw;
    overflow: auto;
}
p.ExpensesPositionView__name {
    font-family: "Inter";
    font-style: normal;
    font-weight: 400;
    font-size: 5vw;
    color: #000000;
}
p.ExpensesPositionView__coast {
    font-family: "Inter";
    font-style: normal;
    font-weight: 400;
    font-size: 4vw;
    color: #474747;
}
.ExpensesPositionView__btn-wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    column-gap: 3vw;
}

.ExpensesCreateView__text-wrapper {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: center;

    width: 60vw;
    overflow: auto;
}
input.ExpensesCreateView__name {
    outline: none;
    border: none;

    max-width: 100%;

    font-family: "Inter";
    font-style: normal;
    font-weight: 400;
    font-size: 5vw;
    color: #000000;
}
input.ExpensesCreateView__coast {
    outline: none;
    border: none;

    max-width: 75%;

    font-family: "Inter";
    font-style: normal;
    font-weight: 400;
    font-size: 4vw;
    color: #474747;
}
</style>