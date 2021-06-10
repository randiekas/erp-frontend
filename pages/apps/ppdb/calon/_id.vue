<template>
	<div>
			<v-app>
				
				<div class="d-flex">
				<v-navigation-drawer>
					<div class="px-4 my-4">
						<v-btn 
							small 
							block
							to="/apps/ppdb/calon"
							exact>
							<v-icon left>mdi-chevron-left</v-icon>
							Kembali
						</v-btn>
					</div>
					<v-divider></v-divider>
					<v-list
						dense
						nav>
						<v-list-item
							v-for="item in items"
							:key="item.title"
							:to="`${item.to}`"
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
			{ title: 'Biodata Calon Siswa', icon: 'mdi-account-tie', to:"biodata" },
			{ title: 'Riwayat Kesehatan', icon: 'mdi-medical-bag', to:"kesehatan" },
			{ title: 'Informasi Wali (Ayah)', icon: 'mdi-account-supervisor', to:"waliayah" },
			{ title: 'Informasi Wali (Ibu)', icon: 'mdi-account-supervisor', to:"waliibu" },
			{ title: 'Informasi Wali', icon: 'mdi-account-supervisor', to:"wali" },
			{ title: 'Berkas', icon: 'mdi-certificate', to:"berkas" },
        ],
    }),
	methods:{
		handleSubmit:()=>{

		}
	}
}
</script>
