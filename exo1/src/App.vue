<template>
  <div>
    <!-- Composant amélioré -->
    <InternationalPhoneNumber 
      v-model="internationalPhoneNumber" 
      :country-code="countryCode" 
      :phone-number="phoneNumber" 
      @update:country-code="countryCode = $event"
      @update:phone-number="phoneNumber = $event"
    />

    <ul>
      <li>country code: {{ countryCode }}</li>
      <li>phone number: {{ phoneNumber }}</li>
      <li>international phone number: {{ internationalPhoneNumber }}</li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from "vue";
import InternationalPhoneNumber from './components/InternationalPhoneNumber.vue';

const countryCode = ref('33'); // Par défaut pour la France
const phoneNumber = ref('');
const internationalPhoneNumber = ref('');

// Mettre à jour countryCode et phoneNumber si internationalPhoneNumber change
watch(internationalPhoneNumber, (newVal) => {
  const match = newVal.match(/^\+(\d{1,2})\s*(\d{0,9})$/);
  if (match) {
    countryCode.value = match[1] ?? '';  // fallback si undefined
    phoneNumber.value = match[2] ?? '';  // fallback si undefined
  }
});

// Mettre à jour internationalPhoneNumber si countryCode ou phoneNumber changent
watch([countryCode, phoneNumber], () => {
  internationalPhoneNumber.value = `+${countryCode.value} ${phoneNumber.value}`;
});
</script>
