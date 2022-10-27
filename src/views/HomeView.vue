<template>
  <div class="home">
    <div class="form-container">
      <div class="title">Register</div>
      <form action="#">
        <div class="user-details">
          <div class="input-box name">
            <label>
              <span class="details">Name: </span>
              <input
                @blur="$v.name.$touch()"
                autofocus
                v-model="name"
                type="text"
                autocomplete="off"
                placeholder="Enter Your Name"
              />
            </label>
            <small v-if="!$v.name.required" class="input-box name text-danger"
              >Please enter a valid name</small
            >
          </div>

          <div class="input-box surname">
            <label>
              <span class="details">Surname: </span>
              <input
                v-model="surname"
                type="text"
                autocomplete="off"
                placeholder="Enter Your Surame"
              />
              <small
                v-if="!$v.surname.required"
                class="input-box surname text-danger"
                >Please enter a valid surname</small
              >
            </label>
          </div>
          <div class="input-box email">
            <label>
              <span class="details">e-mail: </span>
              <input
                @blur="$v.email.$touch()"
                v-model="email"
                type="email"
                autocomplete="off"
                placeholder="Enter Your e-mail"
              />
              <div class="invalid-feedback">
                <small
                  v-if="!$v.email.required"
                  class="input-box email text-danger"
                  >This field is required</small
                >
                <small
                  v-if="!$v.email.email"
                  class="input-box email text-danger"
                  >Please enter a valid e-mail address</small
                >
              </div>
            </label>
          </div>
          <div class="input-box phone">
            <label>
              <span class="details">Phone Number: </span>
              <input
                type="tel"
                autocomplete="off"
                placeholder="+90 (___) ___ __ __"
                v-mask="'+90 (###) ### ## ##'"
                v-model="phone"
              />
              <!-- <input type="text" ref="input" v-mask="'+7 (___) ___ __ __'" /> -->
              <small
                v-if="!$v.phone.required"
                class="input-box email text-danger"
                >Please enter a valid phone</small
              >
            </label>
          </div>
          <div class="input-box cities">
            <label>
              <span class="details">City: </span>
              <input
                v-model="city"
                list="cities"
                autocomplete="off"
                placeholder="Select Your City"
              />
              <datalist required id="cities">
                <option value="Ankara"></option>
                <option value="Istanbul"></option>
                <option value="Izmir"></option>
                <option value="Erzurum"></option>
                <option value="Mugla"></option>
              </datalist>
              <small
                v-if="!$v.city.required"
                class="input-box email text-danger"
                >Please select a city</small
              >
            </label>
          </div>
        </div>
        <div class="button">
          <input type="submit" value="Send" />
        </div>
      </form>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import {
  required,
  email,
  name,
  surname,
  city,
  phone,
} from "vuelidate/lib/validators";
import maxLength from "vuelidate/lib/validators/maxLength";
import minLength from "vuelidate/lib/validators/minLength";

export default {
  name: "HomeView",
  data() {
    return {
      errors: [],
      name: "",
      surname: "",
      email: "",
      phone: "",
      city: "",
    };
  },
  validations: {
    name: {
      required,
      name,
      minLength: minLength(3),
      maxLength: maxLength(25),
    },
    surname: {
      required,
      surname,
      minLength: minLength(2),
      maxLength: maxLength(25),
    },
    email: {
      required,
      email,
    },
    city: {
      required,
      city,
    },
    phone: {
      required,
      phone,
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@600&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}

body {
  display: flex;
  height: 100vh;
  justify-content: center;
  align-items: center;
  padding: 10px;
  background: linear-gradient(135deg, #32daa9, #298692);
}

.form-container {
  max-width: 700px;
  width: 100%;
  background: #fff;
  padding: 25px 30px;
  border-radius: 10px;
}

.form-container .title {
  font-size: 25px;
  font-weight: 500;
  position: relative;
}

.form-container .title::before {
  content: "";
  position: absolute;
  height: 3px;
  width: 105px;
  left: 0;
  bottom: 0;
  background: linear-gradient(135deg, #32daa9, #2d78da);
}

.form-container form .user-details {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin: 20px 0 12px 0;
}

form .user-details .input-box {
  margin-bottom: 15px;
  width: calc(100% / 2 - 20px);
}

.user-details .input-box .details {
  display: block;
  font-weight: 500;
  margin-bottom: 5px;
}

.user-details .input-box input {
  height: 45px;
  width: 100%;
  outline: none;
  border-radius: 5px;
  border: 1px solid #32daa9;
  padding-left: 15px;
  font-size: 16px;
  border-bottom-width: 2px;
  transition: all 0.3s ease;
}

.user-details .input-box input:valid {
  border-color: #32daa9;
}

.user-details .input-box input:focus {
  border-style: groove;
  border-color: #2d78da;
  border-width: 2px;
}

form .button {
  height: 45px;
  margin: 45px 0;
  border-radius: 5px;
}

form .button input {
  height: 100%;
  width: 100%;
  outline: none;
  color: #fff;
  background: linear-gradient(135deg, #32daa9, #2d78da);
  border: none;
  font-size: 18px;
  font-weight: 500;
  letter-spacing: 1px;
  border-radius: 8px;
}

form .button input:hover {
  background: linear-gradient(-135deg, #32daa9, #2d78da);
  cursor: pointer;
}

@media (max-width: 584px) {
  form-container {
    max-width: 100%;
  }

  form .user-details .input-box {
    margin-bottom: 15px;
    width: 100%;
  }

  .form-container form .user-details {
    max-height: 300px;
    overflow-y: scroll;
  }
}

.user-details::-webkit-scrollbar {
  width: 0;
}

.text-danger {
  color: red;
}
</style>
