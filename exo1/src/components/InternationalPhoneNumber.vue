<template>
  <div class="input-wrapper" :class="{ 'is-focus': isFocus }">
    <input 
      type="text" 
      class="country-code" 
      :value="countryCode" 
      maxlength="2"
      @input="onCountryCodeChange" 
      @focus="isFocus = true" 
      @blur="isFocus = false" 
    />
    <input 
      type="text" 
      class="phone-number" 
      :value="phoneNumber" 
      maxlength="9"
      @input="onPhoneNumberChange" 
      @focus="isFocus = true" 
      @blur="isFocus = false" 
    />
  </div>
</template>

<script setup lang="ts">
import { ref, watch, defineProps, defineEmits } from 'vue';

const props = defineProps<{
  modelValue: string,
  countryCode: string,
  phoneNumber: string
}>();

const emit = defineEmits<{
  (e: 'update:modelValue', value: string): void,
  (e: 'update:country-code', value: string): void,
  (e: 'update:phone-number', value: string): void
}>();

const isFocus = ref(false);

const countryCode = ref(props.countryCode);
const phoneNumber = ref(props.phoneNumber);

// Synchronisation props -> local
watch(() => props.countryCode, (val) => countryCode.value = val);
watch(() => props.phoneNumber, (val) => phoneNumber.value = val);

// Émettre la valeur complète
const updateModelValue = () => {
  emit('update:modelValue', `+${countryCode.value} ${phoneNumber.value}`);
};

const onCountryCodeChange = (e: Event) => {
  const value = (e.target as HTMLInputElement).value.slice(0, 2);
  countryCode.value = value;
  emit('update:country-code', value);
  updateModelValue();
};

const onPhoneNumberChange = (e: Event) => {
  const value = (e.target as HTMLInputElement).value.slice(0, 9);
  phoneNumber.value = value;
  emit('update:phone-number', value);
  updateModelValue();
};
</script>

<style scoped>
.input-wrapper {
  display: inline-block;
  border: 1px solid #e1e4e8;
  border-radius: 6px;
  box-shadow: rgba(225, 228, 232, 0.2) 0px 1px 0px 0px inset;
}
.input-wrapper.is-focus {
  border-color: #0366d6;
  box-shadow: rgba(3, 102, 214, 0.3) 0px 0px 0px 3px;
}
input[type="text"] {
  padding: 5px 12px;
  font-size: 14px;
  line-height: 20px;
  color: #000; /* texte noir */
  background-color: #fff; /* fond blanc */
  vertical-align: middle;
  border-radius: 6px;
  outline: none;
  border: none;
}

input.country-code {
  width: 35px;
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
  border-right: 1px solid #e1e4e8;
}
input.phone-number {
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}
</style>
