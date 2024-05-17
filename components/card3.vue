<template>
  <div class="d-flex flex-no-wrap justify-space-between">
    <v-row align="center" justify="center" dense>
      <p v-for="(ksm, i) in jmlKsm.data" :key="i">
      <p v-for="(item, id) in jadwal.data" :key="item.id">
      <p v-if="ksm.Nama_ksm === item.Ksm.Nama_ksm">
      <p v-if="item.Jaga_awal <= formattedTime && item.Jaga_akhir >= formattedTime">
        <v-col cols="12" md="3">
          <v-card variant="tonal" width="300" color="surface-variant" :title="ksm.Nama_ksm"
            append-avatar="data:image/jpeg;base64,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">
            <v-list>
              <v-list-item :key="item.id" :subtitle="item.Nama_petugas" :title="item.Level.Nama_level_igd">
                <template v-slot:prepend>
                  <v-avatar color="blue">
                    <v-icon color="white" icon="mdi-hospital-box"></v-icon>
                  </v-avatar>
                </template>
              </v-list-item>

              <v-list-item :key="item.id" :subtitle="item.Jaga_awal">
              </v-list-item>
              <v-list-item :key="item.id" :subtitle="item.Jaga_akhir">
              </v-list-item>

            </v-list>
          </v-card>
        </v-col>
      </p>

      </p>
      </p>
      </p>

    </v-row>
  </div>
</template>

<script setup>
import { useNow, useDateFormat } from "@vueuse/core";

const variants = ["elevated", "flat", "tonal", "outlined"];
const slides = ["First", "Second", "Third", "Fourth", "Fifth"];

//untuk tampilkan Date time real time
const now = useDateFormat(useNow(), "dddd, DD MM YYYY HH:mm:ss", {
  locales: "id-ID",
});

//untuk pengecekan date time
const realTime = new Date();

const formattedTime = `${realTime.getFullYear()}-${pad(realTime.getMonth() + 1)}-${pad(realTime.getDate())}T${pad(realTime.getHours())}:${pad(realTime.getMinutes())}:${pad(realTime.getSeconds())}`;

const kemarin = `${realTime.getFullYear()}-${pad(realTime.getMonth() + 1)}-${pad(realTime.getDate() - 1)}`;
const besok = `${realTime.getFullYear()}-${pad(realTime.getMonth() + 1)}-${pad(realTime.getDate() + 1)}`;

function pad(number) {
  return number < 10 ? `0${number}` : number.toString();
}


const jadwal = await $fetch(`https://satu.dev.rssa.id/items/data_jadwal_jaga_dokter?filter[Jaga_awal][_between]=[${kemarin},${besok}]&fields=id, Nama_petugas,Ksm.Nama_ksm,Level.Nama_level_igd,Jaga_awal,Jaga_akhir&filter[Level][_neq]=3`)

const jmlKsm = await $fetch(`https://satu.dev.rssa.id/items/daftar_ksm`);


</script>
