<template>
  <button :class="{ changing: isChanging }" @click="emitEditPost(this.postId)">
    <svg viewBox="0 0 12 12" fill="none" xmlns="http://www.w3.org/2000/svg">
      <g clip-path="url(#clip0_20_101)">
        <path
          id="pen"
          d="M2.46834 10.2589L5.49657 9.01138C5.5724 8.96002 5.64822 8.90865 5.69959 8.85973L10.6871 2.77882C10.8388 2.54889 10.8143 2.24558 10.6113 2.06702L8.2435 0.107724C8.04781 -0.0365939 7.74695 -0.0586084 7.55615 0.183552L2.54417 6.26201C2.4928 6.33784 2.46834 6.41367 2.44143 6.49194L1.80546 9.72319C1.77366 10.276 2.2164 10.3714 2.46834 10.2589ZM7.98911 1.19867L9.59128 2.52199L5.24462 7.83238L3.65713 6.51885L7.98911 1.19867ZM3.26331 7.50706L4.34936 8.40721L2.95022 8.98448L3.26331 7.50706Z"
        />
        <path
          v-show="isChanging"
          id="penLine"
          d="M11.4747 10.9707H2.92576C2.92576 10.9707 1.15236 11.0539 1.08632 10.5989C1.08632 10.5744 1.04229 10.4619 1.27222 10.1831C1.45078 9.95313 1.42388 9.64982 1.22085 9.47125C0.990922 9.29269 0.68761 9.3196 0.509047 9.52262C0.0247269 10.1072 -0.102468 10.616 0.127462 11.0759C0.751208 12.2377 2.84993 11.9638 2.95022 11.9882H11.4747C11.7536 11.9882 11.9835 11.7583 11.9835 11.4795C11.986 11.1982 11.756 10.9707 11.4747 10.9707Z"
        />
      </g>
      <defs>
        <clipPath id="clip0_20_101">
          <rect width="12" height="12" fill="white" />
        </clipPath>
      </defs>
    </svg>
  </button>
</template>

<script>
export default {
  name: "ExpensesEditButton",
  props: {
    postId: {
      type: Number,
      required: true,
    },
    isChanging: {
      type: Boolean,
    },
  },
  methods: {
    emitEditPost(id) {
      this.$emit("editPost", id);
    },
  },
};
</script>

<style lang="scss" scoped>
.changing {
  background: #44b549;
  & #pen {
    fill: #ffffff;
    transform-box: fill-box;
    transform-origin: center;
    animation: penDrow 0.5s ease;
  }
  & #penLine {
    fill: #ffffff;
  }
}
@keyframes penDrow {
  0%,
  100% {
    transform: rotate(0);
  }
  50% {
    transform: rotate(-80deg);
  }
}
button {
  transition: 0.2s;
  cursor: pointer;

  padding: 2vw;
  display: grid;
  place-content: center;

  width: 9vw;
  height: 9vw;

  border-radius: 50%;
  border: none;
  background: #117ebe;
  @media (min-width: 420px) {
    padding: 12px;
    width: 50px;
    height: 50px;
  }

  & > svg {
    width: 100%;
    height: auto;
    & path {
      fill: #000000;
    }
  }
}
</style>
