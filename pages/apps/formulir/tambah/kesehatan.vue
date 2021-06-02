<template>
	<div>
        <Head
            title="Kesehatan"
            subtitle="Isi Semua Data Riwayat Kesehatan Kamu"
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
		let model = (await $api.$get(`/api/v1/ppdb/kesehatan/detil/0`)).data
		return {
			model: model || {
                golongan_darah: "-",
                berat_badan: 0,
                tinggi_badan: 0,
            }
		}
	},
	data: () => ({
        isFetching: false,
        dialog: {},
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
		handleSimpan(){
            this.isFetching = true
            let payload     = {}
            this.fields.map((item)=>{
                payload[item.value] = this.model[item.value]!=undefined?this.model[item.value]:''
            })
			this.$api.$post(`/api/v1/ppdb/kesehatan/simpan`, payload).then(async (resp)=>{
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
