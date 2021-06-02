<template>
	<div>
		<!-- <Head 
			title="Dashboard" 
			subtitle="Statistik Penerimaan Peserta Didik Baru"/> -->
		<Head
			title="PPDB"
			subtitle="Module penerimaan peserta didik baru"
			color="text--black"/>
		<v-row justify="center" >
			<CardStats 
				sm="12" 
				md="3"
				title="Total Pengunjung" 
				value="200"/>
			<CardStats 
				sm="12" 
				md="3"
				title="Total Pendaftar" 
				value="200"/>
			<CardStats 
				sm="12" 
				md="3"
				title="Total Penerimaan" 
				value="200"/>
			<CardStats 
				sm="12" 
				md="3"
				title="Total Diterima" 
				value="200"/>
		</v-row>
		<Head 
			title="Memulai" 
			subtitle="Berikut langkah-langkah untuk membuat proses Penerimaan Peserta Didik Baru"
			color="text--black"/>
			
		<CardStep
			:instruksi="instruksi"
			:instruksiAktif="instruksiAktif"/>
		
	</div>
</template>
<script>
export default {
	data: ()=>({
		instruksiAktif:3,
		instruksi:[
			{
				judul: "Setup Proses Penerimaan",
				instruksi: "Membuat Proses Penerimaan, Contoh : Tahun Ajaran 2021/2022",
				to:"/apps/ppdb/proses",
			},
			{
				judul: "Setup Kelompok Penerimaan",
				instruksi: "Membuat Kelompok Penerimaan seperti: Jalur Prestasi, Jalur Umum dll",
				to:"/apps/ppdb/kelompok",
			},
			{
				judul: "Formulir Calon Siswa",
				instruksi: "Kelola data Penerimaan Peserta didik baru",
				to:"/apps/ppdb/calon",
			},
			{
				judul: "Penempatan",
				instruksi: "Menyeleksi siswa yang diterima",
				to:"/apps/ppdb/penempatan",
			},
			{
				judul: "Laporan",
				instruksi: "Melihat Laporan Detil Penerimaan Peserta didik baru",
				to:"/apps/ppdb/laporan",
			}
		]
	})
}
</script>