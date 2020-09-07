<template>
  <div class="app container">
    <div class="app-row row align-items-center">
      <div class="col-sm-8 offset-sm-2">
        <form @submit="submitForm" novalidate>
          <transition name="slide-fade">
            <div v-show="step === 1" class="app-row-step">
              <AttributesForm v-bind:nextStep="nextStep" />
            </div>
          </transition>
          <transition name="slide-fade">
            <div v-show="step === 2" class="app-row-step">
              <AddressForm
                v-bind:nextStep="nextStep"
                v-bind:backStep="backStep"
              />
            </div>
          </transition>
          <transition name="slide-fade">
            <div v-show="step === 3" class="app-row-step">
              <PassportForm
                v-bind:backStep="backStep"
                v-bind:register="submitForm"
              />
            </div>
          </transition>
          <transition name="slide-fade">
            <div v-show="step === 'success'" class="app-row-step">
              <Success />
            </div>
          </transition>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import AttributesForm from './components/AttributesForm';
import AddressForm from './components/AddressForm';
import PassportForm from './components/PassportForm';
import Success from './components/Success';

export default {
  name: 'App',
  components: {
    AttributesForm,
    AddressForm,
    PassportForm,
    Success,
  },
  data: () => ({
    step: 1,
  }),
  methods: {
    nextStep() {
      if (this.step < 3) {
        this.step++;
      }
    },
    backStep() {
      if (this.step > 1) {
        this.step--;
      }
    },
    submitForm(event) {
      event.preventDefault();
      this.step = 'success';
    },
  },
};
</script>

<style lang="scss" scoped>
@import '~bootstrap/dist/css/bootstrap.min.css';

.app {
  height: 100vh;

  &-row {
    height: 100%;

    &-step {
      padding: 10%;
      border: 2px solid black;
      border-radius: 5px;
    }
  }
}
.slide-fade-enter-active {
  transition: all 0.3s ease;
}
.slide-fade-enter {
  transform: translateX(10px);
  opacity: 0;
}
</style>
