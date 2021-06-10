<template>
	<div>
        <Head
            title="Formulir"
            subtitle="Isi Semua Formulir Berikut ini! :"
            color="text--black"/>
		<v-list dense>
            <template
                v-for="(item, i) in items">
                <v-list-item
                :key="`list-${i}`"
                    :to="item.to"
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
		<v-alert
            border="left"
            close-text="Close Alert"
            color="deep-purple accent-4"
            dark>
            Setelah Mengisi semua data, lalu pilih sekolah yang anda ingin masuki
        </v-alert>
	</div>
</template>
<script>
export default {
	layout: 'apps',
	data: () => ({
		valid: false,
		rule:{
			name:[
				v => !!v || 'Username harus diisi',
			],
			password:[
				v => !!v || 'Password harus diisi',
			]
		},
		items: [
			{ title: 'Biodata Calon Siswa', icon: 'mdi-account-tie', to:"/apps/formulir/tambah/biodata" },
			{ title: 'Riwayat Kesehatan', icon: 'mdi-medical-bag', to:"/apps/formulir/tambah/kesehatan" },
			{ title: 'Informasi Wali (Ayah)', icon: 'mdi-account-supervisor', to:"/apps/formulir/tambah/waliayah" },
			{ title: 'Informasi Wali (Ibu)', icon: 'mdi-account-supervisor', to:"/apps/formulir/tambah/waliibu" },
			{ title: 'Informasi Wali', icon: 'mdi-account-supervisor', to:"/apps/formulir/tambah/wali" },
			{ title: 'Berkas', icon: 'mdi-certificate', to:"/apps/formulir/tambah/berkas" },
        ],
    }),
	methods:{
		handleSubmit:()=>{

		}
	}
}
</script>
