<template>
	<div>
		<p class="subtitle-2">Riwayat Kesehatan :</p>
        <Form
            :fields="fields"
            :model="model"/>
	</div>
</template>
<script>
export default {
    async asyncData({ params, $api}){
		let id_akun	    = params.id
        let model		= (await $api.$get(`/api/v1/ppdb/kesehatan/detil/${id_akun}`)).data
		return {
            model
        }
	},
	data: () => ({
		fields:[
            {
                text: 'Golongan Darah',
                value: 'golongan_darah',            
                type: "radio",
                options: [
                    {
                        label: "A",
                        value: "a"
                    },
                    {
                        label: "AB",
                        value: "ab"
                    },
                    {
                        label: "B",
                        value: "b"
                    },
                    {
                        label: "O",
                        value: "o"
                    },
                    {
                        label: "Belum Ada (-)",
                        value: "-"
                    }
                ]
            }, 
            {
                text: 'Berat Badan (kg)',
                value: 'berat_badan',
                type: 'number',
                info: ['Masukan satuan dalam kg']
            }, 
            {
                text: 'Tinggi Badan (cm)',
                value: 'tinggi_badan',
                type: 'number',
                info: ['Masukan satuan dalam cm']
            }, 
            {
                text: 'Riwayat Penyakit',
                value: 'riwayat_penyakit',
                type: 'textarea',
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
