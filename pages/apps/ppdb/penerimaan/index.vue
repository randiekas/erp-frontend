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
						<v-btn small icon v-on:click="handleKonfirmasiHapus(item)">
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
					:items="data"
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
									label="Pilih Tahun Ajaran"/>
								<v-select
									dense
									v-model="tingkatDipilih"
									:items="tingkat"
									label="Pilih Tingkat"/>
								<v-select
									dense
									v-model="kelasDipilih"
									:items="kelas"
									label="Pilih Kelas"/>
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
	},
	data: () => ({
		dipilih: [],
		dialogDelete: false,
		data: [],
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
		tahunajaran: [2020, 2021],
		tahunajaranDipilih: 2021,
		tingkat: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12],
		tingkatDipilih: 10,
		kelas: ['10 Multimedia A', '10 Multimedia B'],
		kelasDipilih: '10 Multimedia A',
    }),
	methods:{
		handleKonfirmasiHapus(){
			// console.log(this)
			this.dialogDelete	= true
		},
		handleCari(){
			this.$api.$get(`/api/v1/ppdb/pendaftaran/data?id_jalur=${this.jalurDipilih}&nama=${this.nama}`).then((resp)=>{
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
