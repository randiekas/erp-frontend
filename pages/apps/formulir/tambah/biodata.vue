<template>
	<div>
        <Head
            title="Biodata"
            subtitle="Isi Semua Data Pribadi Kamu"
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
		let model = (await $api.$get(`/api/v1/ppdb/biodata/detil/0`)).data
		return {
			model: model || {
                kode_pos: 0,
                anak_ke: 0,
                jumlah_saudara: 0,
                jarak_ke_sekolah: 0,
                tanggal_lahir: "2021-01-01",
            }
		}
	},
	data: () => ({
        isFetching: false,
        dialog: {},
		fields:[
            {
                text: 'NO NIK',
                value: 'nik',
                info: ['NIK bisa dilihat di KK / KTP Contoh : 329812837483626'],
            }, 
            {
                text: 'NISN',
                value: 'nisn',
                info: ['Contoh : 1202144193']
            }, 
            {
                text: 'NO UN',
                value: 'un',
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
                type:'radio',
                options: [
                    {
                        label:'Laki - Laki',
                        value:'l',
                    },
                    {
                        label:'Perempuan',
                        value:'p',
                    }
                ]
            }, 
            {
                text: 'Tempat Lahir',
                value: 'tempat_lahir',
                info: ['Contoh : Samarinda'],
            }, 
            {
                text: 'Tanggal Lahir',
                value: 'tanggal_lahir',
                type: "date",
                info: ['Contoh : yyyy-mm-dd'],
            }, 
            {
                text: 'Agama',
                value: 'agama',
                type:'radio',
                options: [
                    {
                        label:'Islam',
                        value:'islam',
                    },
                    {
                        label:'Hindu',
                        value:'hindu',
                    },
                    {
                        label:'Budha',
                        value:'budha',
                    },
                    {
                        label:'Katolik',
                        value:'katolik',
                    },
                    {
                        label:'Protestan',
                        value:'protestan',
                    },
                    {
                        label:'Konghucu',
                        value:'protestan',
                    }
                ]
            }, 
            {
                text: 'Kewarganegaraan',
                value: 'kewarganegaraan',
                type:'radio',
                options: [
                    {
                        label:'WNI',
                        value:'wni',
                    },
                    {
                        label:'WNA',
                        value:'wna',
                    },
                ]
            }, 
            {
                text: 'Anak Ke',
                value: 'anak_ke',
            }, 
            {
                text: 'Jumlah Saudara (Adik/Kakak)',
                value: 'jumlah_saudara',
            }, 
            {
                text: 'Status Anak',
                value: 'status_anak',
                type:'radio',
                options: [
                    {
                        label:'Anak Kandung',
                        value:'kandung',
                    },
                    {
                        label:'Anak Tiri',
                        value:'tiri',
                    },
                    {
                        label:'Lainnya',
                        value:'lainnya',
                    },
                ]
            }, 
            {
                text: 'Bahasa Sehari-hari',
                value: 'bahasa',
                info: ['Contoh : Indonesia, Inggris dll'],
            }, 
            {
                text: 'Alamat',
                value: 'alamat',
                type: 'textarea',
                info: ['Contoh : Gg. lurah no 4 rt/rw 02/2 kecamatan. lawungan. kota bandung. '],
            }, 
            {
                text: 'Kode POS',
                value: 'kode_pos',
                info: ['Contoh : 020123'],
                type: 'number'
            }, 
            {
                text: 'Jarak Ke Sekolah (KM)',
                value: 'jarak_ke_sekolah',
                info: ['Contoh : 20KM'],
                type: 'number'
            }, 
            {
                text: 'Telepon',
                value: 'telepon',
                info: ['Contoh : 0821XXXXXXX'],
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
			this.$api.$post(`/api/v1/ppdb/biodata/simpan`, payload).then(async (resp)=>{
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
