<template>
    <div class="ExpensesCreateView__wrapper">
        <ExpensesCreateButton
            :isVisible="isVisible"
            @addingPost="addingPost"
            @showView="showView"
        />
        <div class="ExpensesCreateView" :class="{ invisible: !isVisible }">
            <div class="ExpensesCreateView__text-wrapper">
                <input
                    v-model="expenseName"
                    class="ExpensesCreateView__name"
                    placeholder="Продукты"
                />
                <input
                    v-model="expenseValue"
                    class="ExpensesCreateView__coast"
                    placeholder="30"
                    type="number"
                />
            </div>
            <div class="ExpensesCreateView__btn-wrapper">
                <ExpensesCancelButton @cancelAdding="cancelAdding" />
                <ExpensesCreateButton
                    class="ExpensesCreateButton_fake"
                    :isVisible="isVisible"
                />
            </div>
        </div>
    </div>
</template>

<script>
import ExpensesCancelButton from "./ExpensesCancelButton.vue";
import ExpensesCreateButton from "./ExpensesCreateButton.vue";

export default {
    name: "ExpensesCreateView",
    components: {
        ExpensesCancelButton,
        ExpensesCreateButton,
    },
    data: () => ({
        expenseName: "",
        expenseValue: 0,
        isVisible: false,
    }),
    methods: {
        cancelAdding() {
            this.expenseName = "";
            this.expenseValue = 0;
            this.isVisible = false;
        },
        showView() {
            this.isVisible = true;
        },
        addingPost() {
            const newPost = {
                name: this.expenseName || "Продукты",
                sum: this.expenseValue,
            };

            this.cancelAdding();
            this.$emit("addingPost", newPost)
        },
    },
};
</script>

<style scoped>
.ExpensesCreateButton_fake {
    opacity: 0;
    margin: 0;
    z-index: 0;
    pointer-events: none;
}
.ExpensesCreateButton__wrapper {
    margin-top: 6vw;
}
.ExpensesCreateView {
    transform-origin: right center;
    transition: 0.5s;
    padding: 3vw;

    display: flex;
    justify-content: space-between;
    align-items: center;

    background: #e6e6e6;
    border-radius: 3vw;
}
.ExpensesCreateView.invisible {
    transition: 0.2s;
    opacity: 0;
    transform: scaleX(0);
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

    padding-left: 2vw;
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

    padding-left: 2vw;
    max-width: 75%;

    font-family: "Inter";
    font-style: normal;
    font-weight: 400;
    font-size: 4vw;
    color: #474747;
}
.ExpensesCreateView__btn-wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    column-gap: 3vw;
}
</style>