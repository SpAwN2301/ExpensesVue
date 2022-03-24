<template>
  <div class="ExpensesToast">
      {{ this.message }}
  </div>
</template>

<script>
export default {
    name: "ExpensesToast",
    props: {
        message: {
            type: String,
            default: ""
        }
    }
}
</script>

<style>
.ExpensesToast {
    position: absolute;
    z-index: 5;
    top: 0;
    left: 50%;
    transform: translate(-50%, 0);

    width: 80%;
    padding: 2vw;
}
</style>