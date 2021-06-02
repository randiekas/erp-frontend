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
			title: "Proses",
			subtitle: "Kelola Proses Penerimaan Peserta Didik Baru",
			headers: [
				{
					text: 'Nama Proses',
					value: 'proses',
					info: ['Nama proses PPDB, Contoh : Penerimaan Siswa Baru Tahun 2021']
				}, 
				{
					text: 'Kode Awalan',
					value: 'kode',
					type: 'number',
					info: ['Kode Awalan No Pendaftaran, Contoh : 2021'],
				}, 
				{
					text: 'Jumlah Penerimaan',
					value: 'jumlah_penerimaan',
					type: 'number',
					info: ['Jumlah siswa yang diterima, Contoh: 400']
				}, 
				{
					text: 'Keterangan',
					value: 'Keterangan tambahan pada proses ini',
				}, 
				{
					text: 'Status',
					value: 'status',
					type: 'switch'
				}, 
				{
					text: 'Aksi',
					value: 'aksi',
					form: false
				}
			],
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
			]
		}
    }),
	methods:{
		
	}
}
</script>
