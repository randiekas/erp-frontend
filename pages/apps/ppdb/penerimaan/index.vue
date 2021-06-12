<template>
	<div>
		<Head 
			title="Penerimaan" 
			subtitle="Kelola data Penerimaan peserta didik baru "
			color="text--black"/>
		<div>
		<v-row>
			<v-col sm="12" md="7" cols="12">
				<v-data-table
					dense
					v-model="dipilih"
					:headers="headers"
					:items="data"
					item-key="name"
					class="elevation-1 mt-4"
					height="65vh">
					<template v-slot:top>
						<v-row class="mx-2 pt-4">
							<v-col sm="12" md="3" cols="12">
								<v-select
									dense
									v-model="jalurDipilih"
									:items="jalur"
									label="Pilih Jalur"
									item-value="id"
									item-text="nama"/>
							</v-col>
							<v-col sm="12" md="6" cols="12">
								<v-text-field
									dense
									v-model="nama"
									label="Nama"
									v-on:keyup.enter="handleCari"/>
							</v-col>
							<v-col sm="12" md="3" cols="12" class="align-center justify-center d-flex">
								<v-btn 
									small
									block
									v-on:click="handleCari">
									Tampilkan
									<v-icon small right>
										mdi-account-search-outline
									</v-icon>
								</v-btn>
							</v-col>
						</v-row>
					</template>
					<template v-slot:[`item.status`]="{item}">
						<v-switch v-model="item.status" readonly class="mt-0" style="height:-webkit-fill-available"/>
					</template>
					<template v-slot:[`item.dibuat`]="{item}">
						{{$moment(item.dibuat).format('DD MMM, HH:mm:ss')}}
					</template>
					<template v-slot:[`item.aksi`]="{item}">
						<v-btn 
							small 
							icon 
							:to="`/apps/ppdb/calon/${item.id_akun}/biodata`">
							<v-icon small>
								mdi-information
							</v-icon>
						</v-btn>
						<v-btn small icon v-on:click="handleTambahSiswa(item)">
							<v-icon small>
								mdi-account-plus
							</v-icon>
						</v-btn>
					</template>
				</v-data-table>
			</v-col>
			<v-col sm="12" md="5" cols="12">
				<v-data-table
					dense
					v-model="dipilih"
					:headers="headersDiterima"
					:items="dataSiswa"
					item-key="name"
					class="elevation-1 mt-4"
					height="65vh">
					<template v-slot:top>
						<v-row class="mx-2 pt-4">
							<v-col sm="12" md="12" cols="12">
								<v-select
									dense
									v-model="tahunajaranDipilih"
									:items="tahunajaran"
									item-value="value"
									item-text="label"
									label="Pilih Tahun Ajaran"
									v-on:change="handleUpdateDataKelas"/>
								<v-select
									dense
									v-model="tingkatDipilih"
									:items="tingkat"
									label="Pilih Tingkat"
									v-on:change="handleUpdateDataKelas"/>
								<v-select
									dense
									v-model="kelasDipilih"
									:items="kelas"
									item-value="id"
									item-text="nama"
									label="Pilih Kelas"/>
								<v-btn 
									small
									block
									v-on:click="handleUpdateDataSiswa">
									<v-icon small left>
										mdi-account-search-outline
									</v-icon>
									Tampilkan
								</v-btn>
							</v-col>
							<!-- <v-col sm="12" md="12" cols="12" class="align-center justify-center d-flex">
								<v-btn 
									small
									block
									v-on:click="handleCari"
									icon>
									<v-icon small right>
										mdi-account-search-outline
									</v-icon>
								</v-btn>
							</v-col> -->
						</v-row>
					</template>
					<template v-slot:[`item.aksi`]="{item}">
						<v-btn small icon v-on:click="handleKonfirmasiHapus(item)">
							<v-icon small>
								mdi-account-remove
							</v-icon>
						</v-btn>
					</template>
				</v-data-table>
			</v-col>
		</v-row>
		</div>
		<!-- dialog -->
        <v-dialog
			v-model="isFetching"
			hide-overlay
			persistent
			width="300"
			>
			<v-card
				color="primary"
				dark
			>
				<v-card-text>
				Menyimpan ...
				<v-progress-linear
					indeterminate
					color="white"
					class="mb-0"
				></v-progress-linear>
				</v-card-text>
			</v-card>
		</v-dialog>
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
		<!-- untuk popup konfirmasi delete -->
		<v-dialog v-model="dialogDelete" max-width="500px">
			<v-card>
				<v-card-title class="headline">Apakah anda yakin ingin membatalkan penerimaan siswa ini ?</v-card-title>
				<v-card-actions>
				<v-spacer></v-spacer>
				<v-btn color="blue darken-1" text @click="dialogDelete=false">Batal</v-btn>
				
				<v-btn color="blue darken-1" text @click="handleHapus">OK</v-btn>
				<v-spacer></v-spacer>
				</v-card-actions>
			</v-card>
		</v-dialog>
	</div>
</template>
<script>
export default {
	async asyncData({ $api }) {
		let jalur = (await $api.$get(`/api/v1/ppdb/jalur/data`)).data
		return {
			nama:'',
			jalurDipilih:jalur[0].id,
			jalur
		}
	},
	mounted: function(){
		this.handleCari()
		this.handleUpdateDataKelas()
	},
	data: () => ({
		dipilih: [],
		dialogDelete: false,
		data: [],
		dataSiswa: [],
		modal:false,
		dialog:{},
		siswaDipilih:{},
		isFetching:false,
		headers: [
			{ text: 'NIK', value: 'nik' },
			{ text: 'Nama', value: 'nama_lengkap' },
			{ text: 'Daftar', value: 'dibuat' },
			{ text: 'Telepon', value: 'telepon' },
			{ text: '', value: 'aksi' },
		],
		headersDiterima: [
			{ text: 'NIK', value: 'nik' },
			{ text: 'Nama', value: 'nama_lengkap' },
			{ text: '', value: 'aksi' },
		],
		sekolah: ['SMKN 11 Bandung', 'SMPN 11 Bandung'],
		proses: ['umum', 'afirmasi', 'beasiswa'],
		tahunajaran: [
			{
				label:'Tahun Ajaran 2021/2022',
				value:1,
			},
		],
		tahunajaranDipilih: 1,
		tingkat: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12],
		tingkatDipilih: 6,
		kelas: [],
		kelasDipilih: 0,
    }),
	methods:{
		handleKonfirmasiHapus(item){
			// console.log(this)
			this.siswaDipilih	= item
			this.dialogDelete	= true
		},
		handleCari(){
			this.$api.$get(`/api/v1/ppdb/pendaftaran/data?status=3&id_jalur=${this.jalurDipilih}&nama=${this.nama}`).then((resp)=>{
				this.data	= resp.data
			})
			// console.log(this)
			// this.dialogDelete	= true
		},
		handleUpdateDataKelas: async function (){
            let data 	= (await this.$api.$get(`/api/v1/akademik/kelas/data?id_tahun_ajaran=${this.tahunajaranDipilih}&tingkat=${this.tingkatDipilih}`)).data
            this.kelas	= data
			if(data.length>0){
				this.kelasDipilih=data[0].id
			}
        },
		handleUpdateDataSiswa: async function (){
            let data 		= (await this.$api.$get(`/api/v1/akademik/siswa/data?id_kelas=${this.kelasDipilih}`)).data
            this.dataSiswa	= data
        },
		handleHapus(){
			this.dialogDelete	= false
			this.isFetching 	= true
			this.$api.$get(`/api/v1/akademik/siswa/hapus/${this.kelasDipilih}/${this.siswaDipilih.id}`).then(async (resp)=>{
                this.isFetching = false
                this.dialog     = {
                    message: resp.message,
                    status: resp.status
                }
				this.modal		= true
				if(resp.status){
					this.handleUpdateDataSiswa()
                    // this.dialogForm     = false
                    // this.handleUpdateData()
                    // this.$nuxt.refresh()
				}
			})
			
		},
		handleTambahSiswa: function(item){
			this.isFetching 	= true
			const payload		= {
				id_kelas:this.kelasDipilih,
				id_akun:item.id_akun,
			}
			this.$api.$post('/api/v1/akademik/siswa/buat', payload).then(async (resp)=>{
                this.isFetching = false
                this.dialog     = {
                    message: resp.message,
                    status: resp.status
                }
				this.modal		= true
				if(resp.status){
					this.handleUpdateDataSiswa()
                    // this.dialogForm     = false
                    // this.handleUpdateData()
                    // this.$nuxt.refresh()
				}
			})
		}
	}
}
</script>
