<template>
  <div class="ExpensesToast" :class="{ toastAppear : isToastAppear }">
      {{ this.message }}
  </div>
</template>

<script>
export default {
    name: "ExpensesToast",
    props: {
        isToastAppear: {
            type: Boolean,
        },
        message: {
            type: String,
            default: ""
        }
    },
}
</script>

<style>
.ExpensesToast {
    transition: .5s;
    position: absolute;
    z-index: 5;
    top: 0;
    left: 50%;
    transform: translate(-50%, -100%);

    width: 80%;
    padding: 2vw;
}
.toastAppear {
    animation: 5s toastAppear ease;
}

@keyframes toastAppear {
    0%, 100% {
        transform: translate(-50%, -100%);
    }
    10%, 90% {
        transform: translate(-50%, 0);
    } 
}
</style>