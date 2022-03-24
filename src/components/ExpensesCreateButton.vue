<template>
    <button @click="clickHandler" :class="{ confirm: isVisible }">
        <span></span>
        <span></span>
    </button>
</template>

<script>
export default {    
    name: "ExpensesCreateButton",
    props: {
        isVisible: {
            type: Boolean
        }
    },
    methods: {
        clickHandler() {
            if (this.isVisible) {
                this.$emit('addingPost')
            } else {
                this.$emit('showView')
            }
        }
    }
};
</script>

<style scoped>
button {
    margin: 13vw 3vw -13vw auto;
    position: relative;
    z-index: 2;
    cursor: pointer;

    padding: 2vw;
    display: grid;
    place-content: center;

    width: 9vw;
    height: 9vw;

    border-radius: 50%;
    border: none;
    background: #44B549;
}
button > span {
    transition: .2s;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);

    background: #ffffff;
}
button > span:nth-child(1) {
    width: 8%;
    height: 50%;
        transform-origin: bottom center;
}
button > span:nth-child(2) {
    height: 8%;
    width: 50%;
        transform-origin: center center;
}

button.confirm > span:nth-child(1) {
    transform: translate(-50%,-65%) rotate(-45deg) scaleY(.5);
}
button.confirm > span:nth-child(2) {
    transform: translate(-25%,-44%) rotate(-45deg) scaleY(.9);
}
</style>