<template>
  <div class="form">
    <input type="checkbox" class="checkbox" :id="id" :checked="copyValue" @click.stop="updateValue"/>
    <label :for="id" :style="{'--d': size + 'px'}">
      <svg viewBox="0,0,50,50">
        <path d="M5 30 L 20 45 L 45 5"></path>
      </svg>
    </label>
  </div>
</template>

<script>
  export default {
    name: 'checkbox',
    props: {
      size: Number,
      value: Boolean
    },
    data () {
      return {
        copyValue: this.value ? true : false,
        id: Math.random().toString(64).substr(2)
      }
    },
    methods: {
      updateValue () {
        this.copyValue = !this.copyValue
        this.$emit('input', this.copyValue)
      }
    }
  }
</script>

<style scoped>
  input {
    position: absolute;
    opacity: 0;
  }
  input:checked + label svg path {
    stroke-dashoffset: 0;
  }
  input:focus + label {
    transform: scale(1.03);
  }

  .checkbox + label {
    display: block;
    border: 2px solid #333;
    width: var(--d);
    height: var(--d);
    border-radius: 4px;
    cursor: pointer;
    transition: all .2s ease;
  }
  .checkbox + label:active {
    transform: scale(1.05);
    border-radius: 30px;
  }
  .checkbox + label svg {
    pointer-events: none;
  }
  .checkbox + label svg path {
    fill: none;
    stroke: #333;
    stroke-width: 4px;
    stroke-linecap: round;
    stroke-linejoin: round;
    stroke-dasharray: 100;
    stroke-dashoffset: 100;
    transition: all 350ms cubic-bezier(1, 0, 0.37, 0.91);
  }
</style>
