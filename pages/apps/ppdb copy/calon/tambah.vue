<template>
	<div>
		<Head 
			title="Tambah" 
			subtitle="Tambah Proses Penerimaan Peserta Didik Baru"
			back
			color="text--black"/>
			<v-app>
				
				<div class="d-flex">
				<v-navigation-drawer>
					<v-alert dense border="left" type="error" outlined class="mx-2 my-2">
						<small>Isi <b>4 Informasi</b> dibawah ini</small>
					</v-alert>
					<v-divider></v-divider>
					<v-list
						dense
						nav
					>
						<v-list-item
							v-for="item in items"
							:key="item.title"
							:to="`/apps/ppdb/calon/tambah${item.to}`"
							link
							color="primary"
							>
							<v-list-item-icon>
								<v-icon>{{ item.icon }}</v-icon>
							</v-list-item-icon>

							<v-list-item-content>
								<v-list-item-title>{{ item.title }}</v-list-item-title>
							</v-list-item-content>
						</v-list-item>
					</v-list>
				</v-navigation-drawer>
				<v-main style="min-height:100vh">
					<v-container>
					<v-col class="mx-auto">
						<nuxt/>
					</v-col>
					</v-container>
				</v-main>
				</div>
			</v-app>
	</div>
</template>
<script>
export default {
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
			{ title: 'Biodata Calon Siswa', icon: 'mdi-account-tie', to:"" },
			{ title: 'Riwayat Kesehatan', icon: 'mdi-medical-bag', to:"/kesehatan" },
			{ title: 'Informasi Wali (Ayah)', icon: 'mdi-account-supervisor', to:"/waliayah" },
			{ title: 'Informasi Wali (Ibu)', icon: 'mdi-account-supervisor', to:"/waliibu" },
			{ title: 'Informasi Wali', icon: 'mdi-account-supervisor', to:"/wali" },
			{ title: 'Ijazah', icon: 'mdi-certificate', to:"/ijazah" },
        ],
    }),
	methods:{
		handleSubmit:()=>{

		}
	}
}
</script>
