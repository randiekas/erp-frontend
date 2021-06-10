<template>
	<div>
		<p class="subtitle-2">Informasi Orang Tua (Ibu)</p>
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
        let model		= (await $api.$get(`/api/v1/ppdb/ibu/detil/${id_akun}`)).data
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
                text: 'Nama',
                value: 'nama',
                info: ['Contoh : Marsudi']
            }, 
            {
                text: 'Tempat Lahir',
                value: 'tempat_lahir',
                info: ['Contoh : Bandung, Jakarta, Cimahi'],
            }, 
            {
                text: 'Tanggal Lahir',
                value: 'tanggal_lahir',
                type: "date",
                info: ['Contoh : yyyy-mm-dd'],
            }, 
            {
                text: 'Pendidikan Terakhir',
                value: 'pendidikan',
                type:'radio',
                options: [
                    {
                        label:'Tidak Sekolah',
                        value:'tidak',
                    },
                    {
                        label:'SD',
                        value:'sd',
                    },
                    {
                        label:'SMP',
                        value:'smp',
                    },
                    {
                        label:'SMA',
                        value:'sma',
                    },
                    {
                        label:'Sarjana (S1)',
                        value:'sarjana',
                    },
                    {
                        label:'Magister (S2)',
                        value:'magister',
                    },
                    {
                        label:'Doktor (S3)',
                        value:'doktor',
                    },
                ]
            }, 
            {
                text: 'Pekerjaan',
                value: 'pekerjaan',
                type:'radio',
                options: [
                    {
                        label:'Buruh',
                        value:'buruh',
                    },
                    {
                        label:'Karyawan Swasta',
                        value:'swasta',
                    },
                    {
                        label:'Nelayan',
                        value:'nelayan',
                    },
                    {
                        label:'Pedagang Besar',
                        value:'pedagang_besar',
                    },
                    {
                        label:'Pedagang Kecil',
                        value:'pedagang_kecil',
                    },
                    {
                        label:'Pensiunan',
                        value:'pensiunan',
                    },
                    {
                        label:'Petani',
                        value:'petani',
                    },
                    {
                        label:'Peternak',
                        value:'peternak',
                    },
                    {
                        label:'PNS/TNI/Polri',
                        value:'pns',
                    },
                    {
                        label:'Sudah Meninggal',
                        value:'meninggal',
                    },
                    {
                        label:'Tenaga Kerja Indonesia',
                        value:'TKI',
                    },
                    {
                        label:'Tidak Bekerja',
                        value:'tidak_bekerja',
                    },
                    {
                        label:'Wiraswasta',
                        value:'wiraswasta',
                    },
                    {
                        label:'Wirausaha',
                        value:'wirausaha',
                    },
                    {
                        label:'Lainnya',
                        value:'lainnya',
                    },
                ]
            }, 
            {
                text: 'Penghasilan',
                value: 'penghasilan',
                info: ['Contoh : 2000000'],
                type: 'number',
            }, 
            {
                text: 'Email Ibu',
                value: 'email',
                info: ['Contoh : marsudi@gmail.com'],
            }, 
            {
                text: 'Telepon Ibu',
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
