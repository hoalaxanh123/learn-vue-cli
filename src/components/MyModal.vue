<template lang="">
  <teleport to=".modals">
    <div class="modal-background" @click.self="handleClick">
      <div class="modal anim-show">
        <div class="modal-container">
          <div class="modal-header">{{ header }}</div>
          <div class="modal-body">
            <slot>Do you want to do something?</slot>
            <slot name="customs"></slot>
          </div>
          <div class="modal-footer">
            <button class="btn-primary" :value="true" @click="handleClick">
              Yes
            </button>
            <button :value="false" @click="handleClick">No</button>
          </div>
        </div>
      </div>
    </div>
  </teleport>
</template>

<script lang="ts">
  import { defineComponent } from 'vue'

  export default defineComponent({
    props: {
      header: {
        type: String,
        required: true,
      },
    },
    emits: ['handle-modal'],
    methods: {
      handleClick(e: any) {
        const selected = e.srcElement._value
        this.$emit('handle-modal', selected)
      },
    },
  })
</script>
<style scoped>
  @keyframes show {
    0% {
      display: block;
      opacity: 0.2;
      transform: scale(0.3) translateY(-50%);
    }
    100% {
      display: block;
      opacity: 1;
      transform: scale(1) translateY(0);
    }
  }

  .modal-background {
    position: fixed;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    background: rgba(0, 0, 0, 0.5);
  }
  .anim-show {
    animation: show 500ms linear;
    animation-fill-mode: forwards;
  }

  .modal {
    max-width: 400px;
    margin: 100px auto;
    border: 1px solid rgb(253, 223, 223);
    text-align: left;
    border-radius: 10px;
    background-color: rgb(255, 250, 250);
    padding: 20px 30px;
  }
  .modal-header,
  .modal-body {
    border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  }
  .modal-header {
    padding: 5px 0px;
    font-weight: bold;
  }
  .modal-body {
    padding: 20px 5px;
  }
  .modal-footer {
    text-align: right;
    padding-top: 5px;
  }
  button {
    border: 1px solid rgb(253, 223, 223);
    margin: 5px;
    min-width: 70px;
  }
  button:hover {
    background-color: rgb(208, 229, 248);
  }
  .btn-primary {
    background-color: rgb(84, 207, 238);
  }
  .btn-primary:hover {
    background-color: rgb(223, 239, 243);
  }
</style>
