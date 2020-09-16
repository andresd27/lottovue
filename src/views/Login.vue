<template>
  <div class="wrap-login row wrap justify-center">
    <div class="q-pa-md self-center box-login">
      <div class="container">
        <q-avatar size="80px" >
          <img src="../assets/lotto-logo.png" />
        </q-avatar>
        <div class="q-pa-md form-header self-center">
          <p>Webapp-Manejo de loterias y juegos</p>
          <p>En Costa Rica</p>
        </div>
      </div>
      <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md form-body">
        <q-input
          filled
          v-model="username"
          label="Tu Usuario *"
          hint="Usuario de acceso a la plataforma lotto de webd"
          lazy-rules
          :rules="[ val => val && val.length > 0 || 'No digitaste ningun usuario']"
        />

        <q-input
          filled
          v-model="password"
          label="Tu Password *"
          :type="isPwd ? 'password' : 'text'"
          lazy-rules
          :rules="[val => val && val.length > 0 || 'No digitaste password alguno']"
        >
          <template v-slot:append>
            <q-icon
              :name="isPwd ? 'visibility_off' : 'visibility'"
              class="cursor-pointer"
              @click="isPwd = !isPwd"
            />
          </template>
        </q-input>

        <q-toggle v-model="accept" label="Acepto los terminos y condiciones de uso" />

        <div>
          <q-btn label="Ingresar" type="submit" color="primary" />
          <q-btn label="Resetear" type="reset" color="primary" flat class="q-ml-sm" />
        </div>
      </q-form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: null,
      password: null,
      isPwd: true,

      accept: false,
    };
  },

  methods: {
    onSubmit() {
      if (this.accept !== true) {
        this.$q.notify({
          color: "red-5",
          textColor: "white",
          icon: "warning",
          message:
            "Por favor, Necesitas aceptar los terminos y condiciones primero",
        });
      } else {
        this.$q.notify({
          color: "green-4",
          textColor: "white",
          icon: "cloud_done",
          message: "Bienvenido al LottoG by Webdgroup.com",
        })
        this.$router.push('/home')
      }
    },

    onReset() {
      this.username = null;
      this.password = null;
      this.accept = false;
    },
  },
};
</script>

<style scoped>
.wrap-login {
  height: 100vh;
  background: #4286f4; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #3a6073,
    #4286f4
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #3a6073,
    #4286f4
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}

.box-login {
  background-color: aliceblue;
  max-width: 400px;
  height: 500px;
  border-radius: 14px;
  box-shadow: 5px 7px 25px #adb5bd85;
  margin-left: 15px;
  margin-right: 15px;
}

.container{
  display: flex;
  flex-wrap: nowrap;
}

.form-body {
  margin-top: 20px;
}
</style>
