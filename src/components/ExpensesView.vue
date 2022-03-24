<template>
    <div class="ExpensesView">
        <ExpensesCreateView @addingPost="addPost" />
        <ExpensesListView
            :posts="posts"
            @deletePost="deletePost"
            @editPost="editPost"
        />
    </div>
</template>

<script>
import ExpensesCreateView from "./ExpensesCreateView.vue";
import ExpensesListView from "./ExpensesListView.vue";

export default {
    name: "ExpensesView",
    components: {
        ExpensesCreateView,
        ExpensesListView,
    },
    data: () => ({
        posts: [],
        isToastVisible: false,
        toastMsg: "",
    }),
    methods: {
        async getPosts() {
            const response = await fetch(
                "https://new.maincore.ru/api/test/expense"
            );

            if (response.ok) {
                const postsFromFetch = await response.json();
                this.posts = [...postsFromFetch];
                console.log();
            } else {
                this.msg = `An error has occured: ${response.status}`;
            }
        },
        getPost(id) {},

        async deletePost(id) {
            const response = await fetch(
                `https://new.maincore.ru/api/test/expense/${id}`,
                {
                    method: "DELETE",
                }
            );
            this.getPosts();
        },

        async editPost(editablePost) {
            editablePost.expense_at = this.getNowDate;
            console.log(editablePost.id);
            try {
                const response = await fetch(
                    `https://new.maincore.ru/api/test/expense/${editablePost.id}`,
                    {
                        method: "PUTCH",
                        body: JSON.stringify(editablePost),
                        headers: {
                            "Content-Type": "application/json",
                        },
                    }
                );
                const json = await response.json();
                this.toastMsg = "Позиция успешно изменена!";
            } catch (error) {
                this.toastMsg = error;
            }
            this.getPosts();
        },

        async addPost(postObj) {
            postObj.id = this.posts.length;
            postObj.expense_at = this.getNowDate;

            try {
                const response = await fetch(
                    `https://new.maincore.ru/api/test/expense`,
                    {
                        method: "POST",
                        body: JSON.stringify(postObj),
                        headers: {
                            "Content-Type": "application/json",
                        },
                    }
                );
                const json = await response.json();
                this.toastMsg = "Позиция успешно добавлена!";
            } catch (error) {
                this.toastMsg = error;
            }
            this.getPosts();
        },
    },
    computed: {
        getNowDate() {
            const d = new Date();
            const curr_date = d.getDate();
            const curr_month = d.getMonth() + 1;
            const curr_year = d.getFullYear();
            const curr_hour = d.getHours();
            const curr_minutes = d.getMinutes();

            return (
                curr_year +
                "-" +
                curr_month +
                "-" +
                curr_date +
                " " +
                curr_hour +
                ":" +
                curr_minutes
            );
        },
    },
    mounted() {
        this.getPosts();
    },
};
</script>


<style scoped>
</style>
