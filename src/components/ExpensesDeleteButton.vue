<template>
    <button @click="emitDeletePost(this.postId)">
        <svg viewBox="0 0 12 12" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path
                d="M11.6005 1.74414H10.6496H8.5652V0H3.43487V1.74414H1.35043H0.39949V2.78737H1.42923L2.12471 12H9.87543L10.5709 2.78737H11.6006V1.74414H11.6005ZM4.4781 1.04323H7.52197V1.74414H4.4781V1.04323ZM8.908 10.9568H3.09214L2.47538 2.78737H3.43487H8.5652H9.52469L8.908 10.9568Z"
                fill="black"
            />
            <path
                d="M6.41733 4.56886H5.58274V9.17521H6.41733V4.56886Z"
                fill="black"
            />
            <path
                d="M4.81771 4.56886H3.98312V9.17521H4.81771V4.56886Z"
                fill="black"
            />
            <path
                d="M8.01695 4.56886H7.18237V9.17521H8.01695V4.56886Z"
                fill="black"
            />
        </svg>
    </button>
</template>

<script>
export default {
    name: "ExpensesDeleteButton",
    props: {
        postId: {
            type: Number,
            required: true,
        },
    },
    methods: {
        emitDeletePost(id) {
            this.$emit("deletePost", id);
        },
    },
};
</script>

<style lang="scss" scoped>
button {
    cursor: pointer;

    padding: 2vw;
    display: grid;
    place-content: center;

    width: 9vw;
    height: 9vw;

    border-radius: 50%;
    border: none;
    background: #ec3536;
    @media (min-width: 420px) {
        padding: 12px;
        width: 50px;
        height: 50px;
    }
    & > svg {
        width: 100%;
        height: auto;
    }
}
</style>