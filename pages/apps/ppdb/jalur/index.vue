<template>
	<div>
		<Crud
			:crud="crud"/>
	</div>
</template>
<script>
export default {
	data: () => ({
		crud:{
			title: "Jalur",
			subtitle: "Kelola Jalur Penerimaan Peserta Didik Baru",
			apiData: '/api/v1/ppdb/jalur/data',
			apiTambah: '/api/v1/ppdb/jalur/buat',
			apiUbah: '/api/v1/ppdb/jalur/update',
			apiHapus: '/api/v1/ppdb/jalur/hapus',
			headers: [
				{
					text: 'Nama Jalur',
					value: 'nama',
					info: ['Nama Jalur, contoh: afirmasi,  preastasi, Zonasi']
				}, 
				{
					text: 'Kapasitas',
					value: 'kapasitas',
					type: 'number',
					info: ['Jumlah siswa yang akan diterima, contoh: 100']
				}, 
				{
					text: 'Terisi',
					value: 'terisi',
					type: 'number',
					info: ['Jumlah siswa yang sudah diterima sementara, Contoh: 10']
				},
				{
					text: 'Aksi',
					value: 'aksi',
					form: false
				}
			],
		}
    }),
	methods:{
		
	}
}
</script>
