<template>
    <button @click="emitCancelAdding">
        <span></span>
        <span></span>
    </button>
</template>

<script>
export default {
    name: "ExpensesCancelButton",
    methods: {
        emitCancelAdding() {
            this.$emit("cancelAdding");
        },
    },
};
</script>

<style lang="scss" scoped>
button {
    position: relative;
    cursor: pointer;

    padding: 2vw;
    display: grid;
    place-content: center;

    width: 9vw;
    height: 9vw;
    transform: rotate(45deg);

    border-radius: 50%;
    border: none;
    background: #161616;
    @media (min-width: 420px) {
        padding: 12px;
        width: 50px;
        height: 50px;
    }
    & > span {
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);

        background: #ffffff;

        &:nth-child(1) {
            width: 8%;
            height: 50%;
        }
        &:nth-child(2) {
            height: 8%;
            width: 50%;
        }
    }
}
</style>