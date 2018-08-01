<template>
  <div class="form">
    <input type="checkbox" class="checkbox" :id="id" @click.stop="updateValue"/>
    <label :for="id" :style="checkboxStyle">
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
      value: Boolean,
      borderWidth: {
        type: Number,
        default: 2
      },
      borderColor: {
        type: String,
        default: '#333333'
      }
    },
    data () {
      return {
        id: Math.random().toString(36).substr(2),
        checkboxStyle: {
          'border': `${this.borderWidth}px solid ${this.borderColor}`,
          '--d': this.size + 'px'
        }
      }
    },
    methods: {
      updateValue () {
        this.$emit('input', !this.value)
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
  label {
    margin: auto;
    position: relative;
  }
  svg {
    position: absolute;
    left: 0;
    top: 0;
  }
  .checkbox + label {
    display: block;
    width: var(--d);
    height: var(--d);
    border-radius: 4px;
    cursor: pointer;
    transition: all .2s ease;
  }
  .checkbox + label:active {
    transform: scale(1.05);
    border-radius: 10px;
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
