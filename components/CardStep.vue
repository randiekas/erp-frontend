<template>
    <v-stepper v-model="instruksiAktif" vertical>
        <template v-for="(item, index) in instruksi">
            <v-stepper-step :key="`step_${index}`" :step="index+1" :complete="index+1<instruksiAktif">
                {{ item.judul }}
            </v-stepper-step>
            <v-stepper-content :key="`konten_${index}`" :step="instruksiAktif">
                <p>
                    <small>{{ item.instruksi }}</small>
                </p>
                <v-btn 
                    :to="item.to"
                    color="primary">
                    Buka
                </v-btn>
                <!-- <v-btn text @click="instruksiAktif += 1">
                    Selesai
                </v-btn> -->
            </v-stepper-content>
        </template>
    </v-stepper>
</template>
<script>
export default {
    props: ['instruksi', 'instruksiAktif', 'sm', 'md']
}
</script>