<template>
  <div>
    <h4>Шаг 2</h4>
    <div class="fieldset">
      <input
        type="date"
        class="form-control"
        id="date"
        name="date"
        v-model="step2Data.date"
        placeholder="Дата"
        @change="checkBirth"
        required
      >
    </div>
    <div class="fieldset" v-if="!step2Data.image">
      <input
        type="file"
        accept="image/.jpg, .png"
        class="change-profile-image"
        @change="onFileChange"
        value="Загрузите изображение"
      >
    </div>
    <div v-else>
      <button
        class="delete-profile-image"
        color="secondary"
        icon="delete"
        @click="removeImage"
      >Удалить изображение</button>
    </div>
    <p v-if="errors.length">
      <span v-bind="error in errors">{{ error }}</span>
    </p>
  </div>
</template>

<script>
export default {
  name: 'Step2',
  data() {
    return {
      errors: [],
    };
  },
  props: ['currentStep', 'step2Data'],
  methods: {
    onFileChange(e) {
      const files = e.target.files || e.dataTransfer.files;
      if (!files.length) {
        return;
      }
      this.createImage(files[0]);
    },
    createImage(file) {
      const reader = new FileReader();
      const vm = this;

      reader.onload = (e) => {
        vm.step2Data.image = e.target.result;
      };
      reader.readAsDataURL(file);
    },
    removeImage() {
      this.step2Data.image = '';
    },
    checkBirth() {
      this.errors = [];
      if (!this.step2Data.date) {
        this.errors.push('Укажите возраст');
      } else if (!this.validBirth(this.step2Data.date)) {
        this.errors.push('Укажите корректный возраст больше 18 лет');
      }
      if (!this.errors.length) {

      }
    },
    validBirth(bday) {
      console.log(bday);
      const dateString = bday;
      const parts = dateString.split('-'); // not testing if the format is correct here
      const now = new Date();
      // var birthday = new Date(now.getFullYear(),parts[1]-1,parts[0]);
      const age = now.getFullYear() - parts[0];
      console.log(age);

      // if (now<birthday) age--;
      if (age < 18) {
        console.log('You must be over 18 to register');
        return false;
      }
      // other validation
      return true;
    },
  },
};
</script>

<style>
input[type="text"],
input[type="email"],
input[type="date"],
input[type="file"],
textarea {
  box-sizing: border-box;
  width: 100%;
  border: 1px solid #ccc;
  background: #fff;
  margin: 0 0 5px;
  padding: 10px;
}

.fieldset {
  border: medium none !important;
  margin: 0 0 10px;
  min-width: 100%;
  padding: 0;
  width: 100%;
}

button {
  cursor: pointer;
  width: 100%;
  border: none;
  background: #4caf50;
  color: #fff;
  margin: 0 0 5px;
  padding: 10px;
  font-size: 15px;
}

h4 {
  margin: 5px 0 15px;
  display: block;
  font-size: 13px;
  font-weight: 400;
}
</style>
