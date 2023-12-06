<template>
    <button
      :style="{ 'background-color': bgColor }"
      :class="{ highlight: isWinningSlot }"
      @click="slotClicked"
    >
      <fa-icon v-show="mark === 0" icon="fa-solid fa-x" />
      <fa-icon v-show="mark === 1" icon="fa-regular fa-circle" />
    </button>
  </template>
  
  <script>
  export default {
    name: "MarkSlot",
    props: {
      turnNum: Number,
      id: Number,
      winningCombination: Array,
    },
    data() {
      return {
        mark: -1,
        bgColor: "var(--clr-faded)",
      };
    },
    computed: {
      isWinningSlot() {
        return this.winningCombination.includes(this.id); // No need to parseInt
      },
    },
    watch: {
      turnNum: {
        immediate: true,
        handler() {
          this.mark = this.turnNum % 2;
          switch (this.mark) {
            case 0:
              this.bgColor = "var(--clr-acc-x)";
              break;
            case 1:
              this.bgColor = "var(--clr-acc-o)";
              break;
            default:
              this.bgColor = "var(--clr-faded)";
          }
        },
      },
    },
    methods: {
      slotClicked() {
        this.$emit("slot-clicked", this.id);
      },
    },
  };
  </script>
  
  <style scoped>
  button {
    font-size: 2rem;
    width: 3rem;
    height: 3rem;
    padding: 0;
  }
  
  .highlight {
    color: white;
  }
  </style>
  