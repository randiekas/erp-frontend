<template>
	<div>
		<p class="subtitle-2">Informasi Orang Tua Wali (Jika Ada)</p>
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
            text: 'Nama',
            value: 'nisn',
            info: ['Contoh : Marsudi']
        }, 
        {
            text: 'Status',
            value: 'no_un',
        }, 
        {
            text: 'Tempat Lahir',
            value: 'nama_lengkap',
			info: ['Contoh : Bandung, Jakarta, Cimahi'],
        }, 
		{
            text: 'Tanggal Lahir',
            value: 'nama_panggilan',
			info: ['Contoh : tahun/bulan/tanggal'],
        }, 
        {
            text: 'Pendidikan',
            value: 'jenis_kelamin',
        }, 
        {
            text: 'Pekerjaan',
            value: 'pekerjaan',
        }, 
        {
            text: 'Penghasilan',
            value: 'penghasilan',
            info: ['Contoh : 2000000'],
        }, 
        {
            text: 'Email Ortu',
            value: 'email_ortu',
            info: ['Contoh : marsudi@gmail.com'],
        }, 
        {
            text: 'Telepon Ortu',
            value: 'email_ortu',
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
