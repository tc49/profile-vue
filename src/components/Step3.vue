<template>
  <div>
    <h4>Проверка</h4>
    <div class="fieldset">
      <strong>Фамилия:</strong>
      {{ step1Data.userName1 }}
      <br>
      <strong>Имя:</strong>
      {{ step1Data.userName2 }}
      <br>
      <strong>Отчество:</strong>
      {{ step1Data.userName3 }}
      <br>
      <strong>Email:</strong>
      {{ step1Data.email }}
      <br>
      <strong>Телефон:</strong>
      {{ step1Data.phone }}
      <br>
      <strong>Дата рождения:</strong>
      {{ step2Data.date }}
      <br>
      <img class="image" :src="step2Data.image">
      <br>
      <button type="button" @click.prevent="send">Отправить</button>
      <div v-if="showModal" id="modal">
        <div class="modal-mask">
          <div class="wrapper">
            <div class="modal-container">
              Анкета отправлена
              <button class="modal-default-button" @click="showModal = false">OK</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Step3',
  data() {
    return {
      showModal: false,
    };
  },

  props: ['currentStep', 'step1Data', 'step2Data'],
  methods: {
    postPost(url, obj) {
      fetch(url, {
        method: 'post',
        headers: {
          'Content-type': 'application/x-www-form-urlencoded; charset=UTF-8',
        },
        body: JSON.stringify(obj),
      })
        .then((data) => {
          console.log('Request succeeded with JSON response', data);
        })
        .catch((error) => {
          console.log('Request failed', error);
        });
    },
    send() {
      // postPost(url, obj);
      this.showModal = true;
    },
  },
};
</script>

<style>
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
br {
  margin-bottom: 15px;
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
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 300px;
  margin: 10px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.modal-default-button {
  margin-top: 15px;
}

.image {
  border: none;
  margin: 0 0 10px;
  min-width: 100%;
  padding: 0;
  width: 100%;
}
</style>
