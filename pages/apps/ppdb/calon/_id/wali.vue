<template>
	<div>
		<p class="subtitle-2">Informasi Orang Tua Wali (Jika Ada)</p>
        <Form
            :fields="fields"
            :model="model"/>
        <div class="text-right">
            <v-btn 
                type="submit"
                color="primary">
                Simpan
            </v-btn>
        </div>
	</div>
</template>
<script>
export default {
    async asyncData({ params, $api}){
		let id_akun	    = params.id
        let model		= (await $api.$get(`/api/v1/ppdb/wali/detil/${id_akun}`)).data
		return {
            model
        }
	},
	data: () => ({
		dipilih: [],
		dialogDelete: false,
        model: {},
		fields: [
            {
                text: 'Nama Wali',
                value: 'nama',
                info: ['Contoh : Marsudi']
            }, 
            {
                text: 'Alamat Wali',
                value: 'alamat',
                type: 'textarea',
                info: ['Contoh : Gg. lurah no 4 rt/rw 02/2 kecamatan. lawungan. kota bandung. '],
            }, 
            {
                text: 'Email Wali',
                value: 'email',
                info: ['Contoh : marsudi@gmail.com'],
            }, 
            {
                text: 'Telepon Wali',
                value: 'telepon',
                info: ['Contoh : 082126833236'], 
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
