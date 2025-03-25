<script setup>
import { ref } from 'vue';
import { supabase } from '../lib/supabase';

const email = ref('');
const password = ref('');
const errorMessage = ref('');

const signUp = async () => {
  const { error } = await supabase.auth.signUp({ email: email.value, password: password.value });
  if (error) errorMessage.value = error.message;
};

const signIn = async () => {
  const { error } = await supabase.auth.signInWithPassword({ email: email.value, password: password.value });
  if (error) errorMessage.value = error.message;
};
</script>

<template>
  <div class="p-4">
    <input v-model="email" placeholder="Email" class="border p-2 w-full" />
    <input v-model="password" type="password" placeholder="Mot de passe" class="border p-2 w-full mt-2" />
    <button @click="signUp" class="bg-blue-500 text-white p-2 mt-2 w-full">S'inscrire</button>
    <button @click="signIn" class="bg-green-500 text-white p-2 mt-2 w-full">Se connecter</button>
    <p v-if="errorMessage" class="text-red-500">{{ errorMessage }}</p>
  </div>
</template>
