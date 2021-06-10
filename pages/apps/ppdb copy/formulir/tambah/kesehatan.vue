<template>
	<div>
		<p class="subtitle-2">Riwayat Kesehatan :</p>
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
            text: 'Golongan Darah',
            value: 'golongan_darah',            
            type: "radio",
            options: [
                {
                    label: "A",
                    value: "A"
                },
                {
                    label: "AB",
                    value: "AB"
                },
                {
                    label: "B",
                    value: "B"
                },
                {
                    label: "B",
                    value: "B"
                },
                {
                    label: "O",
                    value: "O"
                },
                {
                    label: "Belum Ada (-)",
                    value: "-"
                }
            ]
        }, 
        {
            text: 'Berat Badan',
            value: 'berat_badan',
        }, 
        {
            text: 'Tinggi Badan',
            value: 'tinggi_badan',
        }, 
		{
            text: 'Riwayat Penyakit',
            value: 'riwayat_penyakit',
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
