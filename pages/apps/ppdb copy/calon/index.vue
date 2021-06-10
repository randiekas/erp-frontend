<template>
	<div>
		<Head 
			title="Calon" 
			subtitle="Kelola data pendaftaran / calon siswa"
			color="text--black"/>
		<v-data-table
			dense
			v-model="dipilih"
			:headers="headers"
			:items="data"
			item-key="name"
			show-select
			class="elevation-1 mt-4"
			height="65vh">
			<template v-slot:top>
				<v-row class="mx-2">
					<v-col sm="12" md="3" cols="12">
						<v-select
							:items="proses"
							label="Pilih Jalur"/>
					</v-col>
					<v-col sm="12" md="6" cols="12">
						<v-text-field
							label="Nama"/>
					</v-col>
					<v-col sm="12" md="3" cols="12" class="align-center justify-center d-flex">
						<v-btn block>
							Cari
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
			<template v-slot:[`item.aksi`]="{item}">
				<v-btn small icon v-on:click="handleKonfirmasiHapus(item)">
					<v-icon small>
						mdi-delete
					</v-icon>
				</v-btn>
				<v-btn small icon to="/apps/ppdb/calon/tambah">
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
	data: () => ({
		dipilih: [],
		dialogDelete: false,
		data: [
			{
				id:"1",
				nik: '1202144193',
				nama: 'Randi Eka Setiawan',
				email: 'randiekas@gmail.com',
				telepon: '082126833236',
				jarak: '20',
			},
			{
				id:"1",
				nik: '1202144194',
				nama: 'Athalia Tsania',
				email: 'yasfa@gmail.com',
				telepon: '082126833236',
				jarak: '20',
			},
		],
		headers: [
			{ text: 'NIK', value: 'nik' },
			{ text: 'Nama', value: 'nama' },
			{ text: 'Email', value: 'email' },
			{ text: 'Telepon', value: 'telepon' },
			{ text: 'Jarak', value: 'jarak' },
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
		handleHapus(){
			this.dialogDelete	= false
		}
	}
}
</script>
