<template>
	<div>
		<!-- untuk header -->
		<Head 
			:title="crud.title" 
			:subtitle="crud.subtitle"
            color="text--black"/>

		<v-row>
			<v-col sm="12" md="4" cols="12">
				<v-card>
					<v-card-text>
				<v-row>
				<v-col sm="12" md="12" cols="12">
					<v-select
						dense
						v-model="tahunajaranDipilih"
						:items="tahunajaran"
						label="Pilih Tahun Ajaran"
						item-value="value"
						item-text="label"
						v-on:change="handleUpdateDataKelas"/>
					<v-select
						dense
						v-model="tingkatDipilih"
						:items="tingkat"
						label="Pilih Tingkat"
						v-on:change="handleUpdateDataKelas"/>
					<v-select
						dense
						v-model="kelasDipilih"
						:items="kelas"
						item-value="id"
						item-text="nama"
						label="Pilih Kelas"/>
					<v-btn 
						small
						block
						v-on:click="handleUpdateData">
						<v-icon small left>
							mdi-account-search-outline
						</v-icon>
						Tampilkan
					</v-btn>
				</v-col>
				
				</v-row>
					</v-card-text>
				</v-card>
			</v-col>
			<v-col sm="12" md="8" cols="12">
				<v-data-table
					dense
					:headers="crud.headers.filter((item)=>item.table!=false)"
					:items="data"
					item-key="name"
					class="elevation-1"
					height="65vh">
					<template v-slot:[`item.status`]="{item}">
						<v-switch v-model="item.status" readonly class="mt-0" style="height:-webkit-fill-available"/>
					</template>
					<template v-slot:[`item.aksi`]="{item}">
						<!-- <v-btn small icon v-on:click="handleOpenFormEdit(item)">
							<v-icon small>
								mdi-pencil
							</v-icon>
						</v-btn> -->
						<v-btn small icon v-on:click="handleKonfirmasiHapus(item)">
							<v-icon small>
								mdi-delete
							</v-icon>
						</v-btn>
					</template>
				</v-data-table>
			</v-col>
		</v-row>
		<!-- untuk table -->
        <!-- untuk popup konfirmasi delete -->
		<v-dialog v-model="dialogDelete" max-width="500px">
			<v-card>
				<v-card-title class="headline">Apakah anda yakin ingin menghapus data ini ?</v-card-title>
				<v-card-actions>
				<v-spacer></v-spacer>
				<v-btn color="blue darken-1" text @click="dialogDelete=false">Batal</v-btn>
				
				<v-btn color="blue darken-1" text @click="handleHapus">OK</v-btn>
				<v-spacer></v-spacer>
				</v-card-actions>
			</v-card>
		</v-dialog>
	</div>
</template>
<script>
export default {
	// mounted: function(){
	// 	this.handleUpdateData()	
	// },
	data: () => ({
		isFetching: false,
        dialog: {},
        model: {},
        isFetching:false,
		dialogForm: false,
		dialogDelete: false,
		dialogTitle: '',
		data:[],
		tahunajaran: [
			{
				label:'Tahun Ajaran 2021/2022',
				value:1,
			},
		],
		tahunajaranDipilih:1,

		tingkat: [1,2,3,4,5,6,7,8,9,10,11,12], 
		tingkatDipilih:6,

		kelas: [],
		kelasDipilih: 0,

		crud:{
			title: "Siswa",
			subtitle: "Kelola data siswa",
			apiData: '/api/v1/akademik/siswa/data',
			apiHapus: '/api/v1/akademik/siswa/hapus',
			headers: [
				{
					text: 'NIK',
					value: 'nik',
				},
				{
					text: 'NISN',
					value: 'nisn',	
				},
				{
					text: 'NISN',
					value: 'nisn',
				},
				{
					text: 'Nama Lengkap',
					value: 'nama_lengkap',
				},
				{
					text: 'Telepon',
					value: 'telepon',
				},
				{
					text: 'Aksi',
					value: 'aksi',
					form: false
				}
			],
		}
    }),
	mounted: function(){
		this.handleUpdateDataKelas()
	},
	methods:{
		handleKonfirmasiHapus(item){
			// console.log(this)
            this.model        = Object.assign({}, item)
			this.dialogDelete	= true
		},
		handleHapus(){
            this.isFetching     = true
            this.$api.$get(`${this.crud.apiHapus}/${this.kelasDipilih}/${this.model.id}`).then((resp)=>{
                this.isFetching     = false
                this.dialog     = {
                    message: resp.message,
                    status: resp.status
                }
                if(resp.status){
                    this.dialogDelete	= false
                    this.handleUpdateData()
                    // this.$nuxt.refresh()
				}
                
            })
            
			this.dialogDelete	= false
		},
		handleOpenFormTambah(){
            this.dialogTitle    = "Tambah"
            this.dialogForm     = true
			this.model			= {}
			this.model.id_tahun_ajaran	= this.tahunajaranDipilih
			this.model.tingkat	= this.tingkatDipilih
        },
        handleOpenFormEdit(item){
            this.dialogTitle    = "Edit"
            this.dialogForm     = true
            this.model          = Object.assign({}, item)
        },
        handleUpdateData: async function (){
            let data 		= (await this.$api.$get(`${this.crud.apiData}?id_kelas=${this.kelasDipilih}`)).data
            this.data		= data
        },
        handleSimpan: function(){
			this.isFetching = true
            let payload     = {}
            this.crud.headers.filter((item)=>item.form!=false).map((item)=>{
                payload[item.value] = this.model[item.value]!=undefined?this.model[item.value]:''
            })
            const api = this.model.id?`${this.crud.apiUbah}/${this.model.id}`:this.crud.apiTambah
			this.$api.$post(api, payload).then(async (resp)=>{
                this.isFetching = false
                this.dialog     = {
                    message: resp.message,
                    status: resp.status
                }
				if(resp.status){
                    this.dialogForm     = false
                    this.handleUpdateData()
                    // this.$nuxt.refresh()
				}
			})
		},
		handleUpdateDataKelas: async function (){
            let data 	= (await this.$api.$get(`/api/v1/akademik/kelas/data?id_tahun_ajaran=${this.tahunajaranDipilih}&tingkat=${this.tingkatDipilih}`)).data
            this.kelas	= data
			if(data.length>0){
				this.kelasDipilih=data[0].id
			}
        },
	}
}
</script>
