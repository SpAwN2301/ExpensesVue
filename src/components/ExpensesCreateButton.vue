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
            type: Boolean,
        },
    },
    methods: {
        clickHandler() {
            if (this.isVisible) {
                this.$emit("addingPost");
            } else {
                this.$emit("showView");
            }
        },
    },
};
</script>

<style lang="scss" scoped>
button {
    user-select: none;
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
    background: #44b549;
    @media (min-width: 420px) {
        padding: 12px;
        width: 50px;
        height: 50px;

        margin: auto 12px -63px auto;
    }

    & > span {
        transition: 0.2s;
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);

        background: #ffffff;
        &:nth-child(1) {
            width: 8%;
            height: 50%;
            transform-origin: bottom center;
        }
        &:nth-child(2) {
            height: 8%;
            width: 50%;
            transform-origin: center center;
        }
    }
    &.confirm {
        & > span:nth-child(1) {
            transform: translate(-50%, -65%) rotate(-45deg) scaleY(0.5);
        }
        & > span:nth-child(2) {
            transform: translate(-25%, -44%) rotate(-45deg) scaleY(0.9);
        }
    }
}
</style>