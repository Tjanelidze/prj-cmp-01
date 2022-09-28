<template>
  <base-dialog v-if="InputIsInvalid" title="Invalid Input" @close="confrimError">
    <template #default>
      <p>Unfortunately, at leat one input value is invalid.</p>
      <p>
        PLease check all inputs and make sure you enter at leat a few characters
        into each input field.
      </p>
    </template>
    <template #actions>
      <base-button @click="confrimError">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title" name="title" type="text" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          name="description"
          id="description"
          rows="3"
          ref="descInput"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" type="url" ref="linkInput" />
      </div>
      <div class="form-control">
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
import BaseButton from '../UI/BaseButton.vue';

export default {
  components: { BaseButton },
  inject: ['addResource'],
  data() {
    return {
      InputIsInvalid: false,
    };
  },
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDec = this.$refs.descInput.value;
      const enteredUrl = this.$refs.linkInput.value;

      if (
        enteredTitle.trim() === '' ||
        enteredDec.trim() === '' ||
        enteredUrl.trim() === ''
      ) {
        this.InputIsInvalid = true;
        return;
      }

      this.addResource(enteredTitle, enteredDec, enteredUrl);
    },
    confrimError() {
      this.InputIsInvalid = false;
    },
  },
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
