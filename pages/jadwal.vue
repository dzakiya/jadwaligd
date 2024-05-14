<script setup lang="ts">
    import { useNow, useDateFormat } from '@vueuse/core'
    const now = useDateFormat(useNow(), "dddd, DD MMMM YYYY HH:mm:ss", {locales:'id-ID'})

    const data = await useFetch('https://satu.dev.rssa.id/items/data_jadwal_jaga_dokter')

    const data_ksm = await useFetch('https://satu.dev.rssa.id/items/daftar_ksm')
    

</script>

<template>
{{ data }}

{{ data_ksm }}
</template>