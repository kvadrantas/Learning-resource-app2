<template>
<div>
    <base-dialog v-if="inputIsInvalid" title="Invalid input" @close="confirmError">
        <template #default>
            <div>
                <p>Some of entered data is invalid</p>
                <p>Please check if you have not left empty input fields</p>
            </div>
        </template>
        <template #actions>
            <base-button @click="confirmError">Ok</base-button>
        </template>
    </base-dialog>
    <base-card>
        <h2>Add Resource</h2>
        <form @submit.prevent="submitData">
        <div class="form-control">
            <label for="title">Title</label>
            <input type="text" id="title" name="title" ref="titleInput" />
        </div>
        <div class="form-control">
            <label for="descripotion">Descrtiptioin</label>
            <textarea
            id="descripotion"
            name="descripotion"
            rows="3"
            ref="descriptionInput"
            />
        </div>
        <div class="form-control">
            <label for="link">Link</label>
            <input type="url" id="link" name="link" ref="urlInput" />
        </div>
        <div>
            <base-button type="submit">Add resource</base-button>
        </div>
        </form>
    </base-card>
</div>
</template>

<script>
import BaseDialog from '../UI/BaseDialog.vue';
export default {
  components: { BaseDialog },
  inject: ["addResource"],
  data() {
      return {
          inputIsInvalid: false,
      };
  },
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescritption = this.$refs.descriptionInput.value;
      const enteredURL = this.$refs.urlInput.value;

      if (
        enteredTitle.trim() === "" ||
        enteredDescritption.trim() === "" ||
        enteredURL.trim() === ""
      ) {
        this.inputIsInvalid = true;
        return;
      }
      this.addResource(enteredTitle, enteredDescritption, enteredURL);
    },
    confirmError() {
        this.inputIsInvalid = false;
    }
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
