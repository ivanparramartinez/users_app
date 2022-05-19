<template>
  <div>
    <div id="form">
      <form
        id="login-form"
        class="login-form"
        autocomplete="off"
        role="main"
        v-on:submit.prevent="submit"
      >
        <h2>Agrega un usuario</h2>
        <div>
          <input
            type="email"
            id="email"
            name="email"
            placeholder="Email"
            v-model="email"
          />
        </div>
        <div>
          <input
            type="text"
            id="nombre"
            name="nombre"
            placeholder="Nombre(s)"
            v-model="first_name"
          />
        </div>
        <div>
          <input
            type="text"
            id="apellido"
            name="apellido"
            placeholder="Apellido(s)"
            v-model="last_name"
          />
        </div>
        <div class="fecha_nac">
          <date-picker
            name="fecha_nacimiento"
            v-model="fecha_nacimiento"
            valueType="format"
            placeholder="Fecha de Nacimiento"
            :disabled-date="(date) => date >= new Date()"
          ></date-picker>
        </div>

        <button type="submit">Agregar Usuario</button>
      </form>
    </div>
  </div>
</template>

<script>
import DatePicker from "vue2-datepicker";
import "../assets/css/datepicker.css";

export default {
  name: "UsersForm",
  components: {
    DatePicker,
  },
  data() {
    return {
      today: new Date(),
      email: "",
      first_name: "",
      last_name: "",
      fecha_nacimiento: "",
    };
  },
  computed: {
    formIsValid() {
      return (
        this.email && this.first_name && this.last_name && this.fecha_nacimiento
      );
    },
    calculateAge() {
      const today = new Date();
      console.log(this.fecha_nacimiento);
      const birthDate = new Date(this.fecha_nacimiento);
      console.log(birthDate);
      let age = today.getFullYear() - birthDate.getFullYear();
      const m = today.getMonth() - birthDate.getMonth();
      if (m < 0 || (m === 0 && today.getDate() < birthDate.getDate())) {
        age--;
      }
      console.log(age);
      return age;
    },
  },
  watch: {
    date(newVal) {
      console.log(newVal);
    },
  },
  methods: {
    submit() {
      if (this.formIsValid) {
        this.$emit("addUser", {
          email: this.email,
          first_name: this.first_name,
          last_name: this.last_name,
          birthday: this.fecha_nacimiento,
          age: this.calculateAge,
        });

        this.email = "";
        this.first_name = "";
        this.last_name = "";
        this.fecha_nacimiento = "";
      } else {
        alert("Por favor llena todos los campos");
      }
    },
  },
};
</script>

<style scoped>
#form {
  margin: 0px auto;
  width: 100%;
  background: white;
  border-radius: 0.8rem;
  box-shadow: 0px 2px 15px rgba(0, 0, 0, 0.25);
  padding: 1rem 2rem;
}

#form h2 {
  text-align: center;
  font-size: 1.5rem;
  font-weight: bold;
  padding: 0;
  margin: 0;
}

input {
  width: 100%;
  border: 1px solid #ccc;
  border-radius: 0.8rem;
  padding: 0.5rem 1rem;
  margin: 0.5rem 0;
}

input::placeholder {
  color: rgb(149, 149, 149);
}

input:focus {
  outline: none;
}

button {
  background-color: #fa2727;
  border-radius: 0.8rem;
  padding: 1rem 1rem;
  margin: 0.5rem 0;
  width: 100%;
  color: white;
  border: none;
  cursor: pointer;
  font-weight: bold;
  box-shadow: 0px 2px 15px rgba(0, 0, 0, 0.25);
}

button:disabled {
  background-color: gray;
  cursor: default;
}

button:focus {
  box-shadow: none;
}

button:hover {
  background-color: #be1e1e;
}

button:disabled:hover {
  background-color: gray;
}
</style>