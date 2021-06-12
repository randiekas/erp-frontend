<template>
	<div>
		<Head 
			title="Calon" 
			subtitle="Seleksi calon siswa / peserta didik baru"
			color="text--black"/>
		<v-data-table
			dense
			v-model="dipilih"
			:headers="headers"
			:items="data"
			item-key="name"
			class="elevation-1 mt-4"
			height="65vh">
			<template v-slot:top>
				<v-row class="mx-2">
					<v-col sm="12" md="3" cols="12">
						<v-select
							v-model="jalurDipilih"
							:items="jalur"
							label="Pilih Jalur"
							item-value="id"
							item-text="nama"
							v-on:change="handleCari"/>
					</v-col>
					<v-col sm="12" md="3" cols="12">
						<v-select
							v-model="statusDipilih"
							:items="status"
							label="Pilih Status"
							item-value="id"
							item-text="nama"
							v-on:change="handleCari"/>
					</v-col>
					<v-col sm="12" md="3" cols="12">
						<v-text-field
							v-model="nama"
							label="Nama"
							v-on:keyup.enter="handleCari"/>
					</v-col>
					<v-col sm="12" md="3" cols="12" class="align-center justify-center d-flex">
						<v-btn 
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
			<template v-slot:[`item.dibuat`]="{item}">
				{{$moment(item.dibuat).format('DD MMM, HH:mm:ss')}}
			</template>
			<template v-slot:[`item.aksi`]="{item}">
				<v-btn small icon v-on:click="handleKonfirmasiHapus(item)">
					<v-icon small>
						mdi-delete
					</v-icon>
				</v-btn>
				<v-btn 
					small 
					icon 
					:to="`/apps/ppdb/calon/${item.id_akun}/biodata`">
					<v-icon small>
						mdi-information
					</v-icon>
				</v-btn>
			</template>
		</v-data-table>
		<v-dialog v-model="dialogDelete" max-width="500px">
			<v-card>
				<v-card-title class="headline">Apakah anda yakin ingin menghapus data ini ?</v-card-title>
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
			jalur,
			status: [
				{
					id: 0,
					nama: "Belum Diperiksa",
				},
				{
					id: 1,
					nama: "Diterima",
				},
				{
					id: 2,
					nama: "Ditolak",
				},
				{
					id: 3,
					nama: "Daftar ulang",
				}
			],
			statusDipilih: 0,
		}
	},
	mounted: function(){
		this.handleCari()
	},
	data: () => ({
		
		dipilih: [],
		dialogDelete: false,
		data: [],
		headers: [
			{ text: 'NIK', value: 'nik' },
			{ text: 'Nama', value: 'nama_lengkap' },
			{ text: 'Telepon', value: 'telepon' },
			{ text: 'Jarak ke sekolah', value: 'jarak_ke_sekolah' },
			{ text: 'Tanggal Daftar', value: 'dibuat' },
			{ text: 'Aksi', value: 'aksi' },
		],
		sekolah: ['SMKN 11 Bandung', 'SMPN 11 Bandung'],
		proses: ['umum', 'afirmasi', 'beasiswa'],
    }),
	methods:{
		handleKonfirmasiHapus(){
			// console.log(this)
			this.dialogDelete	= true
		},
		handleCari(){
			this.$api.$get(`/api/v1/ppdb/pendaftaran/data?id_jalur=${this.jalurDipilih}&nama=${this.nama}&status=${this.statusDipilih}`).then((resp)=>{
				this.data	= resp.data
			})
			// console.log(this)
			// this.dialogDelete	= true
		},
		handleHapus(){
			this.dialogDelete	= false
		}
	}
}
</script>
