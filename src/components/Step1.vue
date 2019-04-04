<template>
  <div>
    <h4>Шаг 1</h4>

    <div class="fieldset">
      <input type="text" name="name1" v-model="step1Data.userName1" placeholder="Фамилия">
    </div>
    <div class="fieldset">
      <input type="text" name="name2" v-model="step1Data.userName2" placeholder="Имя">
    </div>
    <div class="fieldset">
      <input type="text" name="name3" v-model="step1Data.userName3" placeholder="Отчество">
    </div>
    <div class="fieldset">
      <span>+7</span>
      <input
        type="tel"
        v-model="step1Data.phone"
        name="phone"
        id="phone"
        placeholder="(555) 555-5555"
        autocomplete="tel"
        maxlength="14"
        class="form-control"
        v-phone
        pattern="[(][0-9]{3}[)] [0-9]{3}-[0-9]{4}"
        required
      >
    </div>
    <div class="fieldset">
      <input
        type="email"
        name="email"
        v-model="step1Data.email"
        placeholder="email"
        @change="checkForm"
      >
    </div>
    <p v-if="errors.length">
      <span v-bind="error in errors">{{ error }}</span>
    </p>
  </div>
</template>

<script>
export default {
  name: 'Step1',
  data() {
    return {
      errors: [],
    };
  },
  props: ['currentStep', 'step1Data'],
  directives: {
    phone: {
      bind(el) {
        el.oninput = function (e) {
          if (!e.isTrusted) {
            return;
          }
          const x = this.value
            .replace(/\D/g, '')
            .match(/(\d{0,3})(\d{0,3})(\d{0,4})/);
          this.value = !x[2]
            ? x[1]
            : `(${x[1]}) ${x[2]}${x[3] ? `-${x[3]}` : ''}`;
          el.dispatchEvent(new Event('input'));
        };
      },
    },
  },
  methods: {
    checkForm() {
      this.errors = [];
      if (!this.step1Data.email) {
        this.errors.push('Укажите электронную почту.');
      } else if (!this.validEmail(this.step1Data.email)) {
        this.errors.push('Укажите корректный адрес электронной почты.');
      }
      if (!this.errors.length) {

      }
    },
    validEmail(email) {
      const re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(email);
    },
  },
};
</script>

<style>
input[type="text"],
input[type="email"],
input[type="tel"],
input[type="url"],
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

h4 {
  margin: 5px 0 15px;
  display: block;
  font-size: 13px;
  font-weight: 400;
}
</style>
