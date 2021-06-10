<template>
	<div>
		<Head 
			title="PPDB" 
			subtitle="Berikut langkah-langkah untuk mendaftar calon siswa baru ke sekolah"
			color="text--black"/>
			
		<CardStep
			:instruksi="instruksi"
			:instruksiAktif="instruksiAktif"/>
		
		<Head 
			title="Calon" 
			subtitle="Kelola data pendaftaran / calon siswa"
			add="/apps/ppdb/calon/tambah"
			:handleDelete="dipilih.length>0 && handleKonfirmasiHapus"
			color="text--black"/>
		
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
				proses: "Penerimaan Siswa Baru 2020",
				kode: "2020",
				jumlah_penerimaan: 300,
				keterangan: "-",
				status: 1,
			},
			{
				id:"2",
				proses: "Penerimaan Siswa Baru 2021",
				kode: "2021",
				jumlah_penerimaan: 320,
				keterangan: "-",
				status: 1,
			},
		],
		headers: [
			{ text: 'Proses', value: 'proses' },
			{ text: 'Kode Awalan', value: 'kode' },
			{ text: 'Jumlah Penerimaan', value: 'jumlah_penerimaan' },
			{ text: 'Keterangan', value: 'keterangan' },
			{ text: 'Status', value: 'status' },
			{ text: 'Aksi', value: 'aksi' },
		],
		sekolah: ['SMKN 11 Bandung', 'SMPN 11 Bandung'],
		proses: ['PPDB 2021'],

		instruksiAktif:1,
		instruksi:[
			{
				judul: "Isi Formulir",
				instruksi: "Isi Formulir pendaftaran beserta biodata anda",
				to:"/apps/ppdb/proses",
			},
			{
				judul: "Pilih Sekolah",
				instruksi: "Pilih sekolah yang ingin anda masukin",
				to:"/apps/ppdb/kelompok",
			},
			{
				judul: "Hasil",
				instruksi: "Tunggu hasil pengumuman penerimaan siswa baru",
				to:"/apps/ppdb/calon",
			},
		]
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
