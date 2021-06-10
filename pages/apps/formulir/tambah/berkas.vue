<template>
	<div>
        <Head
            title="Berkas"
            subtitle="Isi Semua Berkas dibawah ini"
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
		let model = (await $api.$get(`/api/v1/ppdb/berkas/detil/0`)).data
		return {
			model: model || {}
		}
	},
	data: () => ({
        isFetching: false,
        dialog: {},
		fields: [
            {
                text: 'Raport Seluruh Semester (dilegalisir)',
                value: 'raport',
                type: 'file',
                info: ['Gunakan file PDF']
            }, 
            {
                text: 'Akta Keluarga',
                value: 'akta',
                type: 'file',
                info: ['Gunakan file PDF']
            }, 
            {
                text: 'Kartu Keluarga ',
                value: 'kk',
                type: 'file',
                info: ['Gunakan file PDF']
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
			this.$api.$post(`/api/v1/ppdb/berkas/simpan`, payload).then(async (resp)=>{
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
