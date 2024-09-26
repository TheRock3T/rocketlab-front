<template>
  <div class="flex flex-col gap-10">
    <div class="flex flex-row justify-center">
      <UButton color="primary" variant="outline" size="xl" @click="startSpeedTest" :disabled="loading">
        Начать тестирование
      </UButton>
    </div>
    <div class="flex flex-row gap-16 items-start justify-center">
      <div class="flex flex-col gap-2">
        <div class="text-center text-2xl text-white">DEV [BACKEND RESPONSE]</div>
        <UTable :rows="loadingDev ? [] : resultsDev" :columns="columns" :loading="loadingDev"></UTable>
      </div>
      <div class="flex flex-col gap-2">
        <div class="text-center text-2xl text-white">PREPROD [BACKEND RESPONSE]</div>
        <UTable :rows="loadingPreprod ? [] : resultsPreprod" :columns="columns" :loading="loadingPreprod"></UTable>
      </div>
      <div class="flex flex-col gap-2">
        <div class="text-center text-2xl text-white">PROD [BACKEND RESPONSE]</div>
        <UTable :rows="loading ? [] : results" :columns="columns" :loading="loading"></UTable>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useFetch } from '#app';

const columns = [
  { key: 'url', label: 'Ссылка' },
  { key: 'time', label: 'Время загрузки [Секунды]' },
  { key: 'status', label: 'Статус' }
];

const results = ref([]);
const resultsDev = ref([]);
const resultsPreprod = ref([]);
const loading = ref(false);
const loadingDev = ref(false);
const loadingPreprod = ref(false);
const startSpeedTest = async () => {
  const testdev = async () => {
    const urls = [
      'https://vpodarok.hellishworld.ru',
      'https://vpodarok.hellishworld.ru/universalCard',
      'https://vpodarok.hellishworld.ru/certificate',
      'https://vpodarok.hellishworld.ru/certificate/sertifikat_vpodarok',
      'https://vpodarok.hellishworld.ru/universalCard/showcase',
      'https://vpodarok.hellishworld.ru/universalCard/certificate',
      'https://vpodarok.hellishworld.ru/universalCard/mobile',
      'https://vpodarok.hellishworld.ru/universalCard/bankCard/easycard',
      'https://vpodarok.hellishworld.ru/universalCard/certificate/ozon',
      'https://vpodarok.hellishworld.ru/bonus',
    ];

    loadingDev.value = true;

    try {
      const { data, error } = await useFetch('http://localhost:3001/api/speed-test', {
        method: 'POST',
        body: { urls },
      });

      if (error.value) {
        console.error('Ошибка при отправке запроса:', error.value);
        loadingDev.value = false;
        return;
      }

      resultsDev.value = data.value;
    } catch (err) {
      console.error('Ошибка выполнения запроса:', err);
    } finally {
      loadingDev.value = false;
    }
  }

  const testPreprod = async () => {
    const urls = [
      'https://preprod-vpdrk.hellishworld.ru',
      'https://preprod-vpdrk.hellishworld.ru/universalCard',
      'https://preprod-vpdrk.hellishworld.ru/certificate',
      'https://preprod-vpdrk.hellishworld.ru/certificate/sertifikat_vpodarok',
      'https://preprod-vpdrk.hellishworld.ru/universalCard/showcase',
      'https://preprod-vpdrk.hellishworld.ru/universalCard/certificate',
      'https://preprod-vpdrk.hellishworld.ru/universalCard/mobile',
      'https://preprod-vpdrk.hellishworld.ru/universalCard/bankCard/easycard',
      'https://preprod-vpdrk.hellishworld.ru/universalCard/certificate/ozon',
      'https://preprod-vpdrk.hellishworld.ru/bonus',
    ];

    loadingPreprod.value = true;

    try {
      const { data, error } = await useFetch('http://localhost:3001/api/speed-test', {
        method: 'POST',
        body: { urls },
      });

      if (error.value) {
        console.error('Ошибка при отправке запроса:', error.value);
        loadingPreprod.value = false;
        return;
      }

      resultsPreprod.value = data.value;
    } catch (err) {
      console.error('Ошибка выполнения запроса:', err);
    } finally {
      loadingPreprod.value = false;
    }
  }

  const testProd = async () => {
    const urls = [
      'https://vpodarok.ru',
      'https://vpodarok.ru/universalCard',
      'https://vpodarok.ru/certificate',
      'https://vpodarok.ru/certificate/sertifikat_vpodarok',
      'https://vpodarok.ru/universalCard/showcase',
      'https://vpodarok.ru/universalCard/certificate',
      'https://vpodarok.ru/universalCard/mobile',
      'https://vpodarok.ru/universalCard/bankCard/easycard',
      'https://vpodarok.ru/universalCard/certificate/ozon',
      'https://vpodarok.ru/bonus',
    ];

    loading.value = true;

    try {
      const { data, error } = await useFetch('http://localhost:3001/api/speed-test', {
        method: 'POST',
        body: { urls },
      });

      if (error.value) {
        console.error('Ошибка при отправке запроса:', error.value);
        loading.value = false;
        return;
      }

      results.value = data.value;
    } catch (err) {
      console.error('Ошибка выполнения запроса:', err);
    } finally {
      loading.value = false;
    }
  }

  testdev();
  testPreprod();
  testProd();
};
</script>
