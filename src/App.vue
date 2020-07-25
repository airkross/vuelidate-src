<template>
  <div id="app">
    <form @submit.prevent="formHandle()">
      <div class="wrap">
        <div class="wrap-l">
          <h1>ОСНОВНОЕ</h1>
          <!-- фамилия -->
          <label for="surname">Фамилия*</label>
          <input
            class="main-form-item"
            v-model="mainForm.surname"
            id="surname"
            :class="$v.mainForm.surname.$error?'is-error':'is-valid'"
            type="text"
            placeholder="Фамилия"
          />
          <span v-if="$v.mainForm.surname.$error">Обязательное поле для заполнения</span>
          <!-- имя -->
          <label for="name">Имя*</label>
          <input
            class="main-form-item"
            v-model="mainForm.name"
            id="name"
            :class="$v.mainForm.name.$error?'is-error':'is-valid'"
            type="text"
            placeholder="Имя"
          />
          <span v-if="$v.mainForm.name.$error">Обязательное поле для заполнения</span>
          <!-- отчество -->
          <label for="fathname">Отчество</label>
          <input
            class="main-form-item"
            v-model="mainForm.fathname"
            id="fathname"
            type="text"
            placeholder="Отчество"
          />
          <!-- Дата рождения -->
          <label for="birthday">Дата рождения*</label>
          <input
            class="main-form-item"
            v-model="mainForm.birthday"
            type="date"
            :class="$v.mainForm.birthday.$error?'is-error':'is-valid'"
            id="birthday"
            placeholder="Дата рождения"
          />
          <span v-if="$v.mainForm.birthday.$error">Обязательное поле для заполнения</span>
          <!-- Номер телефона -->
          <label for="phone">Номер телефона</label>
          <input
            class="main-form-item"
            :class="$v.mainForm.phone.$error?'is-error':'is-valid'"
            type="text"
            id="phone"
            v-model="mainForm.phone"
            placeholder="Номер телефона"
          />
          <span
            v-if="$v.mainForm.phone.$error"
          >В номере телефона должно быть 11 цифр. Сейчас {{$v.mainForm.phone.$model.length}} из {{$v.mainForm.phone.$params.minLength.min}}</span>
          <!--  -->
          <label for="gender">Пол</label>
          <input class="main-form-item" type="text" id="gender" placeholder="Пол" />
          <!--  -->
          <label
            class="main-form-item"
            for="groupClients"
          >Группа клиентов* (множественный выбор производится через зажатие кнопки shift)</label>
          <select
            class="main-form-item"
            :class="$v.mainForm.groupClients.$error?'is-error':'is-valid'"
            multiple
            v-model="mainForm.groupClients"
            id="groupClients"
          >
            <option>VIP</option>
            <option>Проблемные</option>
            <option>ОМС</option>
          </select>
          <span v-if="$v.mainForm.groupClients.$error">Обязательное поле для заполнения</span>
          <!--  -->
          <label class="main-form-item" for="doctor">Группа клиентов</label>
          <select class="main-form-item" v-model="mainForm.doctor" id="doctor">
            <option>Иванов</option>
            <option>Захаров</option>
            <option>Чернышева</option>
          </select>
          <!--  -->
          <div class="checked">
            <label for="sms">Не отправлять СМС:</label>
            <input class="main-form-item" v-model="mainForm.sendmsg" id="sms" type="checkbox" />
          </div>
        </div>
        <div class="wrap-r">
          <h1>АДРЕС</h1>
          <label for="index">Индекс</label>
          <input type="text" v-model="mainForm.index" id="index" placeholder="Индекс" />
          <label for="country">Страна</label>
          <input type="text" v-model="mainForm.country" id="country" placeholder="Страна" />
          <label for="country">Область*</label>
          <input type="text" v-model="mainForm.region" id="region" placeholder="Область" />
          <label for="city">Город*</label>
          <input
            type="text"
            v-model="mainForm.city"
            id="city"
            :class="$v.mainForm.city.$error?'is-error':'is-valid'"
            placeholder="Город"
          />
          <span v-if="$v.mainForm.city.$error">Обязательное поле для заполнения</span>
          <label for="street">Улица</label>
          <input type="text" v-model="mainForm.street" id="street" placeholder="Улица" />
          <label for="home">Дом</label>
          <input type="text" v-model="mainForm.home" id="home" placeholder="Дом" />
          <h1>ПАСПОРТ</h1>
          <label class="main-form-item" for="type">Тип документа*</label>
          <select class="main-form-item" v-model="mainForm.type" id="type">
            <option>Паспорт</option>
            <option>Свидетельство о рождении</option>
            <option>Вод. удостоверение</option>
          </select>
          <span v-if="$v.mainForm.type.$error">Обязательное поле для заполнения</span>
          <label for="seria">Серия</label>
          <input type="text" v-model="mainForm.seria" id="seria" placeholder="Серия" />
          <label for="number">Номер</label>
          <input type="text" v-model="mainForm.number" id="number" placeholder="Номер" />
          <label for="issued">Кем выдан</label>
          <input type="text" v-model="mainForm.issued" id="issued" placeholder="Кем выдан " />
          <label for="dateIssued">Дата выдачи*</label>
          <input
            class="main-form-item"
            v-model="mainForm.dateIssued"
            type="date"
            :class="$v.mainForm.dateIssued.$error?'is-error':'is-valid'"
            id="dateIssued"
            placeholder="Дата выдачи"
          />
          <span v-if="$v.mainForm.dateIssued.$error">Обязательное поле для заполнения</span>
        </div>
      </div>

      <!-- ---------------------------------------- -->

      <input type="submit" />
    </form>
  </div>
</template>

<script>
import { required, minLength, maxLength } from "vuelidate/lib/validators";

export default {
  name: "App",
  data() {
    return {
      mainForm: {
        surname: "",
        name: "",
        fathname: "",
        birthday: "",
        phone: "7",
        groupClients: [],
        doctor: "",
        sendmsg: false,
        index: "",
        country: "",
        region: "",
        city: "",
        street: "",
        home: "",
        type: "",
        seria: "",
        number: "",
        issued: "",
      },
    };
  },
  validations: {
    mainForm: {
      dateIssued: {
        required,
      },
      type: {
        required,
      },
      city: {
        required,
      },
      surname: {
        required,
      },
      name: {
        required,
      },
      birthday: {
        required,
      },
      phone: {
        minLength: minLength(11),
        maxLength: maxLength(11),
      },
      groupClients: {
        required,
      },
    },
  },
  methods: {
    formHandle() {
      this.$v.$touch();
      if (!this.$v.mainForm.$error) {
        //   fetch data
        console.log(this.mainForm);
        alert("Новый клиент успешно создан.\nПосмотрите в консоль.");
      }
    },
  },
};
</script>

<style lang="scss">
#app {
  max-width: 1140px;
  margin: 0 auto;
  padding-left: 15px;
  padding-right: 15px;
}
.wrap {
  padding: 50px 30px;
  border: 1px solid rgb(154, 197, 154);
  border-radius: 10px;
  margin-bottom: 25px;
  display: flex;
  justify-content: space-between;
  @media screen and (max-width: 767px) {
    flex-direction: column;
  }
  .wrap-l,
  .wrap-r {
    width: 49%;
    @media screen and (max-width: 767px) {
      width: 100%;
    }
  }
  label {
    font-weight: 700;
    margin-bottom: 10px;
    margin-top: 20px;
    text-transform: uppercase;
  }
  .wrap-l {
    display: flex;
    flex-direction: column;
    @media screen and (max-width: 767px) {
      margin-bottom: 15px;
    }
  }
  .wrap-r {
    display: flex;
    flex-direction: column;
  }
}
form {
  display: flex;
  flex-direction: column;
  width: 100%;
  padding-bottom: 100px;
  .checked {
    display: flex;
    align-items: center;
    input {
      margin-bottom: 0;
    }
  }
  select {
    option {
      height: 40px;
      display: flex;
      align-items: center;
      padding-left: 20px;
      padding-right: 20px;
      font-size: 18px;
      border-bottom: 1px solid rgb(194, 194, 194);
      &:last-child {
        border-bottom: none;
      }
    }
    &.is-valid {
      border: 1px solid rgb(154, 197, 154);
    }
    &.is-error {
      border: 1px solid rgb(179, 20, 20);
    }
  }
  span {
    color: red;
    margin-bottom: 20px;
  }
  input {
    height: 40px;
    border: none;
    margin-bottom: 15px;
    border-bottom: 1px solid rgb(154, 197, 154);
    outline: none;
    cursor: pointer;

    &.is-valid {
      border-bottom: 1px solid rgb(154, 197, 154);
    }
    &.is-error {
      border-bottom: 1px solid rgb(179, 20, 20);
    }
  }
  input[type="submit"] {
    background: none;
    border: 2px solid rgb(154, 197, 154);
    transition: 0.2s;
    border-radius: 5px;
    max-width: 300px;
    width: 100%;
    font-style: 18px;
    text-transform: uppercase;
    font-weight: 700;
    color: rgb(75, 182, 75);
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
    margin-left: auto;
    margin-right: auto;
    &:hover {
      background: rgb(223, 241, 223);
    }
  }
}
</style>
