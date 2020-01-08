<template>
  <div>
    <b-button v-b-modal.modal-1 variant="success">See Results</b-button>
    <b-modal id="modal-1">
      <p class="my-4">You scored: {{ numCorrect }}/{{ numTotal }}</p>
    </b-modal>
  </div>
</template>
<script>
export default {
  props: ["numCorrect", "numTotal"]
};
</script>