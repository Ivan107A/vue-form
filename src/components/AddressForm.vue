<template>
  <div class="row">
    <div class="col-sm-6 form-group">
      <label for="index">Индекс</label>
      <input type="text" class="form-control" id="index" v-model="index" />
    </div>
    <div class="col-sm-6 form-group">
      <label for="country">Страна</label>
      <input type="text" class="form-control" id="country" v-model="country" />
    </div>
    <div class="col-sm-6 form-group">
      <label for="region">Область</label>
      <input type="text" class="form-control" id="region" v-model="region" />
    </div>
    <div class="col-sm-6 form-group">
      <label for="city">Город <span class="text-danger">*</span></label>
      <input
        type="text"
        class="form-control"
        id="city"
        v-model="city"
        @blur="$v.city.$touch()"
        :class="{
          'is-invalid': $v.city.$error,
          'is-valid': !$v.city.$error && $v.city.$model !== '',
        }"
      />
      <div v-if="!$v.city.required" class="invalid-feedback">
        Введите город
      </div>
    </div>
    <div class="col-sm-6 form-group">
      <label for="street">Улица</label>
      <input type="text" class="form-control" id="street" v-model="street" />
    </div>
    <div class="col-sm-6 form-group">
      <label for="house">Дом</label>
      <input type="text" class="form-control" id="house" v-model="house" />
    </div>
    <div class="col-sm-12 text-center mt-3">
      <button type="button" class="btn btn-warning mr-3" @click="backStep">
        Назад
      </button>
      <button
        type="button"
        class="btn btn-info"
        @click="nextStep"
        :disabled="$v.city.$invalid"
      >
        Далее
      </button>
    </div>
  </div>
</template>

<script>
import { required } from 'vuelidate/lib/validators';

export default {
  name: 'AddressForm',
  props: {
    nextStep: Function,
    backStep: Function,
  },
  data: () => ({
    index: '',
    country: '',
    region: '',
    city: '',
    street: '',
    house: '',
  }),
  validations: {
    city: {
      required,
    },
  },
};
</script>
