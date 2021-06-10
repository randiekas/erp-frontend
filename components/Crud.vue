<template>
	<div>
        <!-- untuk header -->
		<Head 
			:title="crud.title" 
			:subtitle="crud.subtitle"
			:handleDelete="dipilih.length>0 && handleKonfirmasiHapus"
            color="text--black">
            <v-btn small
                v-on:click="handleOpenFormTambah">
                <v-icon left>mdi-plus-circle</v-icon>
                Tambah
            </v-btn>
        </Head>
        <!-- untuk table -->
		<v-data-table
			dense
			:headers="crud.headers"
			:items="data"
			item-key="name"
			show-select
			class="elevation-1"
			height="65vh">
			<template v-slot:[`item.status`]="{item}">
				<v-switch v-model="item.status" readonly class="mt-0" style="height:-webkit-fill-available"/>
			</template>
			<template v-slot:[`item.aksi`]="{item}">
				<v-btn small icon v-on:click="handleOpenFormEdit(item)">
					<v-icon small>
						mdi-pencil
					</v-icon>
				</v-btn>
				<v-btn small icon v-on:click="handleKonfirmasiHapus(item)">
					<v-icon small>
						mdi-delete
					</v-icon>
				</v-btn>
			</template>
		</v-data-table>
        <!-- untuk popup form dan edit -->
        <v-dialog
            v-model="dialogForm"
            max-width="500px"
        >
            <v-card>
                <!-- untuk judul dipopup -->
                <v-card-title>
                    <span class="headline">{{ dialogTitle }}</span>
                </v-card-title>

                <v-card-text>
                    <v-container>
                        <Form
                            :fields="crud.headers"
                            :model="model"
                            :isFetching="isFetching"
                            :dialog="dialog"/>
                    </v-container>
                </v-card-text>
                
                <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn
                    color="blue darken-1"
                    text
                    v-on:click="dialogForm=false">
                    Batal
                </v-btn>
                <v-btn
                    color="blue darken-1"
                    text
                    v-on:click="handleSimpan">
                    Simpan
                </v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>

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
    props: ["crud"],
	data: () => ({
        isFetching: false,
        dialog: {},
        model: {},
        isFetching:false,
		dipilih: [],
		dialogForm: false,
		dialogDelete: false,
		dialogTitle: '',
        data: [],
    }),
    mounted(){ 
        this.handleUpdateData()
    },
	methods:{
		handleKonfirmasiHapus(item){
			// console.log(this)
            this.model        = Object.assign({}, item)
			this.dialogDelete	= true
		},
		handleHapus(){
            this.isFetching     = true
            this.$api.$get(`${this.crud.apiHapus}/${this.model.id}`).then((resp)=>{
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
        },
        handleOpenFormEdit(item){
            this.dialogTitle    = "Edit"
            this.dialogForm     = true
            this.model          = Object.assign({}, item)
        },
        handleUpdateData: async function (){
            let data = (await this.$api.$get(this.crud.apiData)).data
            this.data   = data
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
		}
	}
}
</script>
