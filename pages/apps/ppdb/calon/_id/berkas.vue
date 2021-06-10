<template>
	<div>
		<p class="subtitle-2">Berkas-berkas</p>
        <Form
            :fields="fields"
            :model="model"/>
	</div>
</template>
<script>
export default {
    async asyncData({ params, $api}){
		let id_akun	    = params.id
        let model		= (await $api.$get(`/api/v1/ppdb/berkas/detil/${id_akun}`)).data
		return {
            model
        }
	},
	data: () => ({
		fields: [
            {
                text: 'Raport Seluruh Semester (dilegalisir)',
                value: 'raport',
                type: 'openfile',
                info: ['Gunakan file PDF']
            }, 
            {
                text: 'Akta Keluarga',
                value: 'akta',
                type: 'openfile',
                info: ['Gunakan file PDF']
            }, 
            {
                text: 'Kartu Keluarga ',
                value: 'kk',
                type: 'openfile',
                info: ['Gunakan file PDF']
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
