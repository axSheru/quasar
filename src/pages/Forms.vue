<template>
  <q-page class="q-ma-md">
    
    <span class="text-h3">Forms</span>
    <q-separator spaced />

    <div class="row justify-center">

      <q-form
        @submit="onSubmit"
        @reset="onReset"
        class="q-gutter-xs col-sm-12 col-md-6 q-pt-xl"
      >
        <q-input
          filled
          v-model="userForm.email"
          label="Correo electrónico"
          hint="alguien@email.com"
          type="email"
          lazy-rules
          no-error-icon
          :rules="[
            val => val && val.length > 0 || 'Este campo es obligatorio',
            isValidEmail
          ]"
        />

        <q-input
          filled
          type="password"
          v-model="userForm.password1"
          label="Contraseña"
          lazy-rules
          no-error-icon
          :rules="[ val => val && val.length > 0 || 'Este campo es obligatorio']"
        />

        <q-input
          filled
          type="password"
          v-model="userForm.password2"
          label="Repetir contraseña"
          lazy-rules
          no-error-icon
          :rules="[
            val => val && val.length > 0 || 'Este campo es obligatorio',
            isSamePassword
          ]"
        />

        <q-checkbox
          v-model="userForm.conditions"
          label="Acepto los términos y las condiciones de uso."
          :style="[userForm.errorInConditions && !userForm.conditions && 'color: red']"
        />

        <!-- <q-toggle v-model="accept" label="I accept the license and terms" /> -->

        <div class="row justify-end">
          <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
          <q-btn label="Submit" type="submit" color="primary"/>
        </div>
      </q-form>

    </div>

  </q-page>
</template>

<script>
import { useQuasar } from 'quasar'
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'Forms',
  setup() {

    const $q = useQuasar()

    const userForm = ref({
      email: '',
      password1: '',
      password2: '',
      conditions: false,
      errorInConditions: false
    })

    return {
      userForm,

      onSubmit() {

        userForm.value.errorInConditions = false

        if ( !userForm.value.conditions ) {
          $q.notify({
            message: 'Debe de aceptar las condiciones para continuar.',
            color: 'red',
            icon: 'las la-exclamation-circle'
          })
          userForm.value.errorInConditions = true
          return
        }

      },
      onReset() {
        userForm.value = {
          email: '',
          password1: '',
          password2: '',
          conditions: false,
          errorInConditions: false
        }
      },
      isValidEmail( val ) {
          const emailPattern = /^(?=[a-zA-Z0-9@._%+-]{6,254}$)[a-zA-Z0-9._%+-]{1,64}@(?:[a-zA-Z0-9-]{1,63}\.){1,8}[a-zA-Z]{2,63}$/;
          return emailPattern.test(val) || 'El correo no parece ser válido';
      },
      isSamePassword( val ) {
        return ( val === userForm.value.password1 ) || 'Las contraseñas no coinciden.'
      }
    }

  }
})
</script>
