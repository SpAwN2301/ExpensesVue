<template>
    <div class="ExpensesView">
        <ExpensesChart :names="getNames" :costs="getCosts" />
        <div>
            <ExpensesToast :message="toastMsg" />
            <ExpensesCreateView @addingPost="addPost" />
            <ExpensesListView
                :posts="posts"
                @deletePost="deletePost"
                @editPost="editPost"
            />
        </div>
    </div>
</template>

<script>
import ExpensesChart from "./ExpensesChart.vue";
import ExpensesToast from "./ExpensesToast.vue";
import ExpensesCreateView from "./ExpensesCreateView.vue";
import ExpensesListView from "./ExpensesListView.vue";

export default {
    name: "ExpensesView",
    components: {
        ExpensesToast,
        ExpensesCreateView,
        ExpensesListView,
        ExpensesChart,
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
            try {
                const response = await fetch(
                    `https://new.maincore.ru/api/test/expense/${id}`,
                    {
                        method: "DELETE",
                    }
                );
                this.toastMsg = "Позиция успешно удалена!";
            } catch (error) {
                this.toastMsg = error;
            }
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
        getNames() {
            return this.posts.map((a) => a.name);
        },
        getCosts() {
            return this.posts.map((a) => a.sum);
        },
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


<style lang="scss" scoped>
.ExpensesView {
    position: relative;
    padding: 10vw 2vw 2vw 2vw;
    @media (min-width: 420px) {
        display: grid;
        grid-template-columns: 1fr 1fr;
    }
}
</style>
