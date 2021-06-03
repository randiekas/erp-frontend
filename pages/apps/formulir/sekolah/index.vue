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
                    v-on:click="handleKonfirmasi"
                    color="primary"
                    >
                    <v-list-item-icon>
                        <v-icon v-text="item.icon"></v-icon>
                    </v-list-item-icon>
                    <v-list-item-content>
                        <v-list-item-title v-text="item.title"></v-list-item-title>
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
                    <span class="headline">Kirim Formulir ?</span>
                </v-card-title>

                <v-card-text>
                    
                    <p>Apakah anda yakin ingin mengirim berkas pendaftaran ke sekolah ini ?</p>
                    
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
			{ title: 'SD NEGRI KEUREA', icon: 'mdi-school'},
			{ title: 'SD NEGRI 1 Kujangsari', icon: 'mdi-school'},
			{ title: 'SD NEGRI 2 Kujangsari', icon: 'mdi-school'},
        ],
    }),
	methods:{
		handleSubmit:function(){
            // this.isFetching = true
            this.dialog = {
                message: 'Berkas ppdb berhasil dikirimkan ke sekolah, silahkan tunggu hasil pengumuman selanjutnya'
            }
            this.dialogForm = false
		},
        handleKonfirmasi: function(){
            this.dialogForm = true
        }
	}
}
</script>
