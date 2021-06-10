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
			title: "Kelas",
			subtitle: "Kelola data kelas",
			apiData: '/api/v1/ppdb/jalur/data',
			apiTambah: '/api/v1/ppdb/jalur/buat',
			apiUbah: '/api/v1/ppdb/jalur/update',
			apiHapus: '/api/v1/ppdb/jalur/hapus',
			headers: [
				{
					text: 'Tahun Ajaran',
					value: 'id_tahun_ajaran',
					type:'select',
					options: [
						{
							label:'Tahun Ajaran 2021/2022',
							value:'1',
						},
					]
				}, 
				{
					text: 'Tingkat',
					value: 'kapasitas',
					type: 'select',
					options: [1,2,3,4,5,6,7,8,9,10,11,12].map((item)=>{
						return {
							label: item,
							value: item,
						}
					})
				}, 
				{
					text: 'Nama Kelas',
					value: 'nama',
					info: ['format : [tingkat, nama kelas, rombel], Contoh: 10 Multimedia 1']
				},
				{
					text: 'Total Siswa',
					value: 'terisi',
					type: 'number',
					info: ['Jumlah siswa yang ada di kelas ini, Contoh: 35']
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
