<template>
	<div>
        <Head
            title="Biodata"
            subtitle="Isi Semua Biodata Wali"
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
		let model = (await $api.$get(`/api/v1/ppdb/wali/detil/0`)).data
		return {
			model: model || {}
		}
	},
	data: () => ({
        isFetching: false,
        dialog: {},
		fields: [
            {
                text: 'Nama Wali',
                value: 'nama',
                info: ['Contoh : Marsudi']
            }, 
            {
                text: 'Alamat Wali',
                value: 'alamat',
                type: 'textarea',
                info: ['Contoh : Gg. lurah no 4 rt/rw 02/2 kecamatan. lawungan. kota bandung. '],
            }, 
            {
                text: 'Email Wali',
                value: 'email',
                info: ['Contoh : marsudi@gmail.com'],
            }, 
            {
                text: 'Telepon Wali',
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
			this.$api.$post(`/api/v1/ppdb/wali/simpan`, payload).then(async (resp)=>{
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
