<template>
  <MyModal v-if="isShowingModal" header="⚠ Warning" @handle-modal="handleModal">
    <div></div>

    <template #customs>
      <h4>The database will be clean and noway to return, are you sure</h4>
      <img src="../assets/vue.svg" style="margin: 0 auto; display: block" />
    </template>
  </MyModal>

  <MyModal
    v-if="isShowing18"
    header="🔞 18+ Only"
    @handle-modal="handleModal18"
  >
    <div></div>
    <template #customs>
      <h4>Are you 18 years old?</h4>
      <img src="../assets/18.jfif" style="width: 100%; border-radius: 10px" />
    </template>
  </MyModal>

  <div>
    <h1>{{ msg }}</h1>
    <button @click="isShowingModal = !isShowingModal">Click Me!</button>
    <h3 v-if="answer">Your answer: {{ answer }}</h3>
    <h3 v-if="enoughYearsOld">Is old enough: {{ enoughYearsOld }}</h3>
  </div>
</template>

<script lang="ts">
  import MyModal from './MyModal.vue'
  import { defineComponent } from 'vue'

  export default defineComponent({
    components: { MyModal },
    props: {
      msg: {
        type: String,
        required: true,
      },
    },
    data() {
      return {
        isShowingModal: false,
        isShowing18: true,
        answer: '',
        enoughYearsOld: '',
      }
    },
    methods: {
      handleModal(returnValue: boolean) {
        this.answer = returnValue ? 'Yes' : 'No'
        this.isShowingModal = !this.isShowingModal
      },
      handleModal18(returnValue: boolean) {
        this.enoughYearsOld = returnValue ? 'Yes' : 'No'
        this.isShowing18 = !this.isShowing18
      },
    },
  })
</script>

<style scoped></style>
