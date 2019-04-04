<template>
  <div class="hello">
    <h3>Анкета</h3>
    <Step1 :step1Data="step1Data" :currentStep="currentStep" v-if="currentStep == 1"/>
    <Step2 :step2Data="step2Data" :currentStep="currentStep" v-if="currentStep == 2"/>
    <Step3
      :step1Data="step1Data"
      :step2Data="step2Data"
      :currentStep="currentStep"
      v-if="currentStep == 3"
    />

    <button
      class="previous"
      type="button"
      v-if="currentStep > 1"
      @click.prevent="goToStep(currentStep-1)"
    >Назад</button>
    <button
      class="next"
      type="button"
      v-if="currentStep < 3"
      @click.prevent="goToStep(currentStep+1)"
    >Далее</button>
  </div>
</template>

<script>
import Step1 from './Step1.vue';
import Step2 from './Step2.vue';
import Step3 from './Step3.vue';

export default {
  name: 'HelloWorld',
  components: {
    Step1,
    Step2,
    Step3,
  },
  data() {
    return {
      errors: [],
      currentStep: 1,
      step1Data: {
        userName1: '',
        userName2: '',
        userName3: '',
        email: '',
        phone: '',
      },
      step2Data: {
        date: '',
        image: '',
      },
    };
  },
  methods: {
    goToStep(step) {
      this.currentStep = step;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.hello {
  max-width: 1200px;
  position: relative;
  background: #f9f9f9;
  padding: 25px;
  padding-bottom: 75px;
  margin: 150px auto;
  box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.2), 0 5px 5px 0 rgba(0, 0, 0, 0.24);
}

.hello h3 {
  display: block;
  font-size: 30px;
  font-weight: 300;
  margin-bottom: 10px;
}
.hello button {
  /* position: absolute; */
  position: relative;
  display: inline-block;
  cursor: pointer;
  width: 40%;
  border: none;
  background: #4caf50;
  color: #fff;
  margin: 0 0 5px;
  padding: 10px;
  font-size: 15px;
}

.previous {
  float: left;
}
.next {
  float: right;
}
</style>
