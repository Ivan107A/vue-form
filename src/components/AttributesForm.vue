<template>
  <div class="row">
    <div class="col-sm-6 form-group">
      <label for="lastname">Фамилия <span class="text-danger">*</span></label>
      <input
        type="text"
        class="form-control"
        id="lastname"
        v-model="lastname"
        @blur="$v.lastname.$touch()"
        :class="{
          'is-invalid': $v.lastname.$error,
          'is-valid': !$v.lastname.$error && $v.lastname.$model !== '',
        }"
      />
      <div v-if="!$v.lastname.$required" class="invalid-feedback">
        Введите фамилию
      </div>
    </div>
    <div class="col-sm-6 form-group">
      <label for="firstname">Имя <span class="text-danger">*</span></label>
      <input
        type="text"
        class="form-control"
        id="firstname"
        v-model="firstname"
        @blur="$v.firstname.$touch()"
        :class="{
          'is-invalid': $v.firstname.$error,
          'is-valid': !$v.firstname.$error && $v.firstname.$model !== '',
        }"
      />
      <div v-if="!$v.firstname.$required" class="invalid-feedback">
        Введите имя
      </div>
    </div>
    <div class="col-sm-6 form-group">
      <label for="middlename">Отчество</label>
      <input
        type="text"
        class="form-control"
        id="middlename"
        v-model="middlename"
      />
    </div>
    <div class="col-sm-6 form-group">
      <label for="dateofbirth"
        >Дата рождения <span class="text-danger">*</span></label
      >
      <input
        type="date"
        class="form-control"
        id="dateofbirth"
        v-model="dateofbirth"
        @blur="$v.dateofbirth.$touch()"
        :class="{
          'is-invalid': $v.dateofbirth.$error,
          'is-valid': !$v.dateofbirth.$error && $v.dateofbirth.$model !== '',
        }"
      />
      <div v-if="!$v.dateofbirth.$required" class="invalid-feedback">
        Введите дату рождения
      </div>
    </div>
    <div class="col-sm-6 form-group">
      <label for="phone">Телефон <span class="text-danger">*</span></label>
      <input
        type="text"
        class="form-control"
        id="phone"
        v-model="phone"
        @blur="$v.phone.$touch()"
        :class="{
          'is-invalid': $v.phone.$error,
          'is-valid': !$v.phone.$error && $v.phone.$model !== '',
        }"
      />
      <div v-if="!$v.phone.required" class="invalid-feedback">
        Введите телефон
      </div>
      <div
        v-else-if="!$v.phone.maxLength || !$v.phone.minLength"
        class="invalid-feedback"
      >
        Длина номера должна быть 11 симолов
      </div>
      <div v-else-if="!$v.phone.isPhone" class="invalid-feedback">
        Номер должен начинаться с 7
      </div>
      <div v-else-if="!$v.phone.numeric" class="invalid-feedback">
        Номер должен содержать только цифры
      </div>
    </div>
    <div class="col-sm-6 form-group">
      <label for="sex">Пол</label>
      <select id="sex" v-model="sex" class="form-control">
        <option value="male">Мужской</option>
        <option value="female">Женский</option>
      </select>
    </div>
    <div class="col-sm-6 form-group">
      <label for="clients_group"
        >Группа клиентов <span class="text-danger">*</span></label
      >
      <select id="clients_group" v-model="clients_group" class="form-control">
        <option value="vip">VIP</option>
        <option value="problem">Проблемные</option>
        <option value="omc">ОМС</option>
      </select>
    </div>
    <div class="col-sm-6 form-group">
      <label for="doctor">Лечащий врач</label>
      <select id="doctor" v-model="doctor" class="form-control">
        <option value="ivanov">Иванов</option>
        <option value="zaharov">Захаров</option>
        <option value="chernisheva">Чернышева</option>
      </select>
    </div>
    <div class="col-sm-12 text-center form-check mb-3">
      <input
        class="form-check-input"
        type="checkbox"
        v-model="sms"
        id="check"
      />
      <label class="form-check-label" for="check">
        Отправлять СМС
      </label>
    </div>
    <div class="col-sm-12 text-center">
      <button
        type="button"
        class="btn btn-info"
        @click="nextStep"
        :disabled="
          $v.lastname.$invalid ||
            $v.firstname.$invalid ||
            $v.dateofbirth.$invalid ||
            $v.phone.$invalid
        "
      >
        Далее
      </button>
    </div>
  </div>
</template>

<script>
import {
  required,
  minLength,
  maxLength,
  numeric,
} from 'vuelidate/lib/validators';

export default {
  name: 'AttributesForm',
  props: {
    nextStep: Function,
  },
  data: () => ({
    lastname: '',
    firstname: '',
    middlename: '',
    dateofbirth: '',
    phone: '',
    sex: 'male',
    clients_group: 'vip',
    doctor: 'ivanov',
    sms: false,
  }),
  validations: {
    lastname: {
      required,
    },
    firstname: {
      required,
    },
    dateofbirth: {
      required,
    },
    phone: {
      required,
      minLength: minLength(11),
      maxLength: maxLength(11),
      numeric,
      isPhone: (phone) => phone.indexOf('7') === 0,
    },
  },
};
</script>
