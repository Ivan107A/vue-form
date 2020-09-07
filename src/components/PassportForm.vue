<template>
  <div class="row">
    <div class="col-sm-6 form-group">
      <label for="documentType"
        >Тип документа <span class="text-danger">*</span></label
      >
      <select id="documentType" v-model="documentType" class="form-control">
        <option value="passport">Паспорт</option>
        <option value="birth certificate">Свидетельство о рождении</option>
        <option value="driver's license">Вод. удостоверение</option>
      </select>
    </div>
    <div class="col-sm-6 form-group">
      <label for="serie">Серия</label>
      <input type="text" class="form-control" id="serie" v-model="serie" />
    </div>
    <div class="col-sm-6 form-group">
      <label for="number">Номер</label>
      <input type="text" class="form-control" id="number" v-model="number" />
    </div>
    <div class="col-sm-6 form-group">
      <label for="who">Кем выдан</label>
      <input type="text" class="form-control" id="who" v-model="who" />
    </div>
    <div class="col-sm-6 form-group">
      <label for="date">Дата выдачи <span class="text-danger">*</span></label>
      <input
        type="date"
        class="form-control"
        id="date"
        v-model="date"
        @blur="$v.date.$touch()"
        :class="{
          'is-invalid': $v.date.$error,
          'is-valid': !$v.date.$error && $v.date.$model !== '',
        }"
      />
      <div v-if="!$v.date.$required" class="invalid-feedback">
        Введите дату выдачи
      </div>
    </div>
    <div class="col-sm-12 text-center mt-3">
      <button type="button" class="btn btn-warning mr-3" @click="backStep">
        Назад
      </button>
      <button
        type="submit"
        class="btn btn-success"
        @click="register"
        :disabled="$v.documentType.$invalid || $v.date.$invalid"
      >
        Зарегистрироваться
      </button>
    </div>
  </div>
</template>

<script>
import { required } from 'vuelidate/lib/validators';

export default {
  name: 'PassportForm',
  props: {
    backStep: Function,
    register: Function,
  },
  data: () => ({
    documentType: 'passport',
    serie: '',
    number: '',
    who: '',
    date: '',
  }),
  validations: {
    documentType: {
      required,
    },
    date: {
      required,
    },
  },
};
</script>
