<template>

     
        <div class="d-flex flex-no-wrap justify-space-between">
          <v-row align="center" justify="center" dense>
            <v-col v-for="(ksm, id) in jmlKsm.data" :key="id" cols="12" md="3"> 
              <v-card
                variant="tonal"
                class="mx-auto"
                height="500"
                width="320"
                color="surface-variant"
                :title="ksm.Nama_ksm"
                :subtitle="ksm.id"
                append-avatar="https://cdn.vuetifyjs.com/images/john.jpg"
                prepend-avatar="https://cdn.vuetifyjs.com/images/logos/v-alt.svg"
              >
                <v-card-text v-for="(jj, id) in jadwal.data" :key="id">
                    {{ jj.Nama_petugas }}
                </v-card-text>
                <template v-slot:actions>
                  <v-btn text="Button"></v-btn>
                </template>
              </v-card>
  
              <div class="text-center text-caption">{{ ksm }}</div>
            </v-col>
          </v-row>
        </div>
     

  
    <v-col v-for="(jdw, id) in jadwal.data[0]" :key="id" cols="12" md="3">
      <v-card
        subtitle="Isi dari card nanti ditaruh sini ya, nama dokter, level, dsb"
        text="TEXT AREA DISINI"
        append-avatar="https://cdn.vuetifyjs.com/images/john.jpg"
        prepend-avatar="https://cdn.vuetifyjs.com/images/logos/v-alt.svg"
      >
      <v-card-title>
          {{jdw}}
        </v-card-title>
      </v-card>
  
      <div class="text-center text-caption">{{ jdw }}</div>
    </v-col>
  
    <pre>{{ jadwal.data[0] }} </pre>
    {{ jadwal.data[0].Nama_petugas }}
    <br />
    {{ jadwal.data.length }}
    <br />
    {{ now }}
  
    {{ tanggal }}
    {{ bulan }}
    {{ tahun }}
  </template>
  
  <script setup>
  import { useNow, useDateFormat } from "@vueuse/core";
  
  const variants = ["elevated", "flat", "tonal", "outlined"];
  const slides = ["First", "Second", "Third", "Fourth", "Fifth"];
  
  //untuk filter tgl
  const now = useDateFormat(useNow(), "dddd, DD MM YYYY HH:mm:ss", {
    locales: "id-ID",
  });
  
  const tgl = ref("");
  const bln = ref("");
  const thn = ref("");
  
  const tanggal = useDateFormat(useNow(), "DD", { locales: "id-ID" });
  const bulan = useDateFormat(useNow(), "MM", { locales: "id-ID" });
  const tahun = useDateFormat(useNow(), "YYYY", { locales: "id-ID" });
  
  tgl.value = tanggal.value;
  bln.value = bulan.value;
  thn.value = tahun.value;
  
  //coba panggil dari dari API
  //const { data: ksm, pending, error } = await useFetch(() => `https://satu.dev.rssa.id/items/data_jadwal_jaga_dokter?fields=Nama_petugas,Ksm.Nama_ksm,Level.Nama_level_igd,Jaga_awal,Jaga_akhir&filter[day(Jaga_awal)][_eq]=14&filter[month(Jaga_awal)][_eq]=05&filter[year(Jaga_awal)][_eq]=2024`)
  //const { data: ksm, pending, error } = await useFetch(() => `https://satu.dev.rssa.id/items/data_jadwal_jaga_dokter?fields=Nama_petugas,Ksm.Nama_ksm,Level.Nama_level_igd,Jaga_awal,Jaga_akhir&filter[day(Jaga_awal)][_eq]=14&filter[month(Jaga_awal)][_eq]=05&filter[year(Jaga_awal)][_eq]=2024`)
  
  const jadwal = await $fetch(
    `https://satu.dev.rssa.id/items/data_jadwal_jaga_dokter?fields=id,Nama_petugas,Ksm.Nama_ksm,Level.Nama_level_igd,Jaga_awal,Jaga_akhir&filter[day(Jaga_awal)][_eq]=14&filter[month(Jaga_awal)][_eq]=05&filter[year(Jaga_awal)][_eq]=2024`
  );

  const jmlKsm = await $fetch(`https://satu.dev.rssa.id/items/daftar_ksm`);
  </script>
  