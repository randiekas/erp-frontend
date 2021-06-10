<template>
	<div>
		<p class="subtitle-2">DATA Pribadi Calon Siswa Baru :</p>
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
	data: () => ({
		dipilih: [],
		dialogDelete: false,
        model:{},
		fields:[
        {
            text: 'NISN',
            value: 'nisn',
            info: ['Contoh : 1202144193']
        }, 
        {
            text: 'NO UN',
            value: 'no_un',
            info: ['Contoh : 1202144193'],
        }, 
        {
            text: 'Nama Lengkap',
            value: 'nama_lengkap',
			info: ['Contoh : Randy Eka XXX XXX'],
        }, 
		{
            text: 'Nama Panggilan',
            value: 'nama_panggilan',
			info: ['Contoh : Randy Eka XXX XXX'],
        }, 
        {
            text: 'Jenis Kelamin',
            value: 'jenis_kelamin',
        }, 
        {
            text: 'Tempat Lahir',
            value: 'tempat_lahir',
            info: ['Contoh : Samarinda'],
        }, 
        {
            text: 'Tanggal Lahir',
            value: 'tanggal_lahir',
            info: ['Contoh : Karangan Estate'],
        }, 
		{
            text: 'Agama',
            value: 'agama',
        }, 
		{
            text: 'Suku',
            value: 'suku',
        }, 
		{
            text: 'Status',
            value: 'status',
        }, 
		{
            text: 'Kondisi',
            value: 'kondisi',
        }, 
		{
            text: 'Kewarganegaraan',
            value: 'kewarganegaraan',
        }, 
		{
            text: 'Anak Ke',
            value: 'anakke',
        }, 
		{
            text: 'Jumlah Saudara Kandung ( Adik/Kakak)',
            value: 'jumlah_saudara',
        }, 
		{
            text: 'Jumlah Saudara Tiri ( Adik/Kakak)',
            value: 'jumlah_saudara_tiri',
        }, 
		{
            text: 'Bahasa Sehari-hari',
            value: 'bahasa',
			info: ['Contoh : Indonesia, Inggris dll'],
        }, 
		{
            text: 'Alamat',
            value: 'alamat',
			info: ['Contoh : Gg. lurah no 4 rt/rw 02/2 kecamatan. lawungan. kota bandung. '],
        }, 
		{
            text: 'Kode POS',
            value: 'kode_pos',
			info: ['Contoh : 020123'],
        }, 
		{
            text: 'Jarak Ke Sekolah',
            value: 'jarak',
			info: ['Contoh : 20KM'],
        }, 
		{
            text: 'Telepon',
            value: 'telepon',
			info: ['Contoh : 0821XXXXXXX'],
        }, 
		{
            text: 'Email',
            value: 'email',
			info: ['Contoh : user@gmail.com'],
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
