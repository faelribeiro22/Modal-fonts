<template>
  <div id="app">
    <button type="button" name="button" @click="showModal = true">Modal</button>
    <modal v-show="showModal"></modal>
  </div>
</template>

<script>
import Modal from './components/Modal.vue';

export default {
  components: {
    Modal
  },
  data() {
    return {
      showModal: false
    }
  }
}
</script>

<style>

</style>
