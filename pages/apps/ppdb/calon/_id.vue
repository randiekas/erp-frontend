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
						<v-btn 
							class="mt-4"
							outlined
							color="success"
							small 
							block
							v-on:click="handleSetStatus(1)"
							exact>
							<v-icon left>mdi-account-check-outline</v-icon>
							Terima
						</v-btn>
						<v-btn 
							class="mt-4"
							outlined
							color="error"
							small 
							block
							v-on:click="handleSetStatus(2)"
							exact>
							<v-icon left>mdi-account-remove-outline</v-icon>
							Tolak
						</v-btn>
						<v-btn 
							class="mt-4"
							outlined
							color="primary"
							small 
							block
							v-on:click="handleSetStatus(3)"
							exact>
							<v-icon left>mdi-card-account-details-outline</v-icon>
							Daftar Ulang
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
				<v-dialog
					v-if="dialog"
					v-model="modal"            
					width="300">
					<v-alert
						v-model="modal"
						border="top"
						color="green accent-4"
						dark
						dismissible
						type="success"
						>
						{{ dialog.message }}
					</v-alert>
				</v-dialog>
			</v-app>
	</div>
</template>
<script>
export default {
	async asyncData({ params, $api}){
		let id_akun	    = params.id
		return {
            id_akun
        }
	},
	data: () => ({
		dialog: {},
		modal: false,
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
		handleSetStatus: function(status){
			const payload = { status }
			this.$api.$post(`/api/v1/ppdb/pendaftaran/updatestatus/${this.id_akun}`, payload).then((resp)=>{
				this.modal	= true
				this.dialog = {
					status: resp.status,
                    message: resp.message
                }
			})
		}
	}
}
</script>
