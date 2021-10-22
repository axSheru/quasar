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
          v-model="name"
          label="Correo electrónico"
          hint="alguien@email.com"
          type="email"
          lazy-rules
          no-error-icon
          :rules="[ val => val && val.length > 0 || 'Este campo es obligatorio']"
        />

        <q-input
          filled
          type="password"
          v-model="age"
          label="Contraseña"
          lazy-rules
          no-error-icon
          :rules="[ val => val && val.length > 0 || 'Este campo es obligatorio']"
        />

        <q-input
          filled
          type="password"
          v-model="age"
          label="Repetir contraseña"
          lazy-rules
          no-error-icon
          :rules="[ val => val && val.length > 0 || 'Este campo es obligatorio']"
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
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Forms'
})
</script>
