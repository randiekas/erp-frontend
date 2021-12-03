<template>
<v-card
    outlined
    class="mb-2">
        <v-card-text class="d-flex">
        <div class="flex-grow-0">
            <v-card class="primary">
                <v-img :src="item.lokasi" width="260"/>
            </v-card>
        </div>
        <div class="flex-grow-1 fill-width">
            <div class="d-flex justify-space-between align-center">
                <div>
                    <v-card-title class="black--text text-truncate">{{ item.nama }}</v-card-title>
                    <v-card-subtitle>{{ item.pelajaran }}</v-card-subtitle>
                </div>
                <v-card outlined rounded="lg">
                    <v-card-text>
                        <v-btn
                            small
                            :to="`/apps/siswa/ujian/${item.id}`"
                            class="primary"
                            rounded="lg">
                            Detail Ujian
                        </v-btn>
                    </v-card-text>
                </v-card>
            </div>
            <v-divider class="m-0 p-0"/>
            <v-row class="mt-0">
                <v-col class="text-center px-4">
                    <span v-if="item.status" class="black--text text-h4">{{ item.nilai }}</span>
                    <v-btn v-else small outlined>Belum Mengerjakan</v-btn>
                </v-col>
                <v-col class="text-center">
                    <my-text
                        title="Jumlah peserta"
                        :subtitle="item.jumlah_peserta||'-'"
                        />
                </v-col>
                <v-col class="text-center">
                    <my-text
                        title="Durasi Ujian"
                        :subtitle="item.durasi||'-'"/>
                </v-col>
                <v-col class="text-center">
                    <my-text
                        title="Mulai ujian"
                        :subtitle="item.mulai_ujian||'-'"/>
                </v-col>
                <v-col class="text-center">
                    <my-text
                        title="Berakhir Ujian"
                        :subtitle="item.berakhir_ujian||'-'"
                        />
                </v-col>
            </v-row>
        </div>
    </v-card-text>
</v-card>
</template>
<script>
export default {
    props: ['item', 'handelHapus', 'handelEditForm']
}
</script>