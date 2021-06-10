<template>
	<div>
		<p class="subtitle-2">Nilai Ijazah</p>
        <Form
            :fields="fields"/>
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
	data: () => ({
		dipilih: [],
		dialogDelete: false,
		fields:[
        {
            text: 'Matematika',
            value: 'golongan_darah',            
            info: ['Contoh : 80'],
        }, 
        {
            text: 'Bahasa Indonesia',
            value: 'berat_badan',
        }, 
        {
            text: 'Bahasa Inggris',
            value: 'tinggi_badan',
			info: ['Contoh : 80'],
        }, 
		{
            text: 'Kimia',
            value: 'riwayat_penyakit',
            info: ['Contoh : 80'],
        }, 
        {
            text: 'Fisika',
            value: 'riwayat_penyakit',
            info: ['Contoh : 80'],
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
