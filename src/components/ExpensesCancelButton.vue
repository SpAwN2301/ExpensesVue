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
        }
    }
};
</script>

<style scoped>
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
}
button > span {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);

    background: #ffffff;
}
button > span:nth-child(1) {
    width: 8%;
    height: 50%;
}
button > span:nth-child(2) {
    height: 8%;
    width: 50%;
}
</style>