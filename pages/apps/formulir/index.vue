<template>
	<div>
		<Head 
			title="PPDB" 
			subtitle="Berikut langkah-langkah untuk mendaftar calon siswa baru ke sekolah"
			color="text--black"/>
		<CardStep
			:instruksi="instruksi"
			:instruksiAktif="instruksiAktif"/>
	</div>
</template>
<script>
export default {
	layout:'apps',
	data: () => ({
		instruksiAktif:1,
		instruksi:[
			{
				judul: "Isi Formulir",
				instruksi: "Isi Formulir pendaftaran beserta biodata anda",
				to:"/apps/formulir/tambah",
			},
			{
				judul: "Pilih Sekolah",
				instruksi: "Pilih sekolah yang ingin anda masuki",
				to:"/apps/formulir/sekolah",
			},
			{
				judul: "Hasil",
				instruksi: "Tunggu hasil pengumuman penerimaan siswa baru",
				to:"/apps/formulir/hasil",
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
