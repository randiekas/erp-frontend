<template>
	<div>
        <Head
            title="Sekolah"
            subtitle="Pilih sekolah yang ingin anda masuki"
            color="text--black"/>
        <Dialog
            :isFetching="isFetching"
            :dialog="dialog"/>
        <v-alert
            border="left"
            close-text="Close Alert"
            color="deep-purple accent-4"
            dark>
            Setelah memilih sekolah, tunggu hasil berikutnya .
        </v-alert>
		<v-list dense>
            <template
                v-for="(item, i) in items">
                <v-list-item
                :key="`list-${i}`"
                    v-on:click="handleKonfirmasi(item)"
                    color="primary"
                    >
                    <v-list-item-icon>
                        <v-icon v-text="item.icon"></v-icon>
                    </v-list-item-icon>
                    <v-list-item-content>
                        <v-list-item-title v-text="item.title"></v-list-item-title>
                        <v-list-item-subtitle v-text="item.subtitle"></v-list-item-subtitle>
                    </v-list-item-content>
                    <v-list-item-action>
                        <v-icon
                            color="grey lighten-1">
                            mdi-chevron-right
                        </v-icon>
                    </v-list-item-action>
                </v-list-item>
                <v-divider :key="i" />
            </template>
		</v-list>
		<v-dialog
            v-model="dialogForm"
            max-width="500px"
        >
            <v-card>
                <!-- untuk judul dipopup -->
                <v-card-title>
                    <span class="headline">Pilih Jalur Pendaftaran</span>
                </v-card-title>

                <v-card-text>
                    <v-container
                        class="px-0"
                        fluid>
                        <v-radio-group v-model="jalurTerpilih" dense>
                        <v-radio
                            off-icon="mdi-checkbox-blank-outline"
                            on-icon="mdi-checkbox-marked-outline"
                            v-for="(item, i) in jalur"
                            :key="i"
                            :label="item.nama"
                            :value="item.id"                            
                        ></v-radio>
                        </v-radio-group>
                    </v-container>
                </v-card-text>
                
                <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn
                    color="blue darken-1"
                    text
                    v-on:click="dialogForm=false">
                    Batal
                </v-btn>
                <v-btn
                    color="blue darken-1"
                    text
                    v-on:click="handleSubmit">
                    Ya, lanjutkan
                </v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
	</div>
</template>
<script>
export default {
	layout: 'apps',
	data: () => ({        
		dialogForm: false,
        isFetching: false,
        dialog: {},
		items: [
			{ id: 1, title: 'SD NEGRI KEUREA', subtitle: 'Jl. Budi Jl. Raya Cilember, Sukaraja, Kec. Cicendo, Kota Bandung, Jawa Barat 40153', icon: 'mdi-school'},
			{ id: 2, title: 'SD NEGRI 1 Kujangsari', subtitle: 'Jl. Budi Jl. Raya Cilember, Sukaraja, Kec. Cicendo, Kota Bandung, Jawa Barat 40153', icon: 'mdi-school'},
        ],
        jalur:[],
        jalurTerpilih: 0,
        sekolahTerpilih: 0,
    }),
	methods:{
		handleSubmit:function(){
            // this.isFetching = true
            const payload   = {
                id_sekolah: this.sekolahTerpilih.id,
                id_jalur: this.jalurTerpilih,
            }
            this.$api.$post(`/api/v1/ppdb/pendaftaran/simpan`, payload).then((resp)=>{
                this.dialog = {
                    message: 'Berkas ppdb berhasil dikirimkan ke sekolah, silahkan tunggu hasil pengumuman selanjutnya'
                }
                this.dialogForm = false
                
            })
            
		},
        handleKonfirmasi: function(item){
            this.sekolahTerpilih    = item
            this.dialogForm         = true
            this.$api.$get(`/api/v1/ppdb/jalur/sekolah/${item.id}`).then((resp)=>{
                this.jalur          = resp.data
                this.jalurTerpilih  = resp.data[0].id
            })
            
        }
	}
}
</script>
