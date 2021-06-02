<template>
	<div>
        <Head
            title="Biodata"
            subtitle="Isi Semua Data Orang Tua (Ayah Kandung)"
            color="text--black"/>
        <Form
            :fields="fields"
            :model="model"
            :isFetching="isFetching"
            :dialog="dialog"/>
        <div class="text-right">
            <v-btn 
                v-on:click="handleSimpan"
                type="submit"
                color="primary">
                Simpan
            </v-btn>
        </div>
	</div>
</template>
<script>
export default {
    layout: 'apps',
    async asyncData({ $api }) {
		let model = (await $api.$get(`/api/v1/ppdb/ayah/detil/0`)).data
		return {
			model: model || {
                penghasilan: 0,
                tanggal_lahir: "2021-01-01",
            }
		}
	},
	data: () => ({
        isFetching: false,
        dialog: {},
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
                text: 'Email Ayah',
                value: 'email',
                info: ['Contoh : marsudi@gmail.com'],
            }, 
            {
                text: 'Telepon Ayah',
                value: 'telepon',
                info: ['Contoh : 082126833236'],
            }, 
        ]
		
    }),
	methods:{
		handleSimpan(){
            this.isFetching = true
            let payload     = {}
            this.fields.map((item)=>{
                payload[item.value] = this.model[item.value]!=undefined?this.model[item.value]:''
            })
			this.$api.$post(`/api/v1/ppdb/ayah/simpan`, payload).then(async (resp)=>{
                this.isFetching = false
                this.dialog     = {
                    message: resp.message,
                    status: resp.status
                }
				if(resp.status){
                    // this.$nuxt.refresh()
				}
			})
		},
	}
}
</script>
