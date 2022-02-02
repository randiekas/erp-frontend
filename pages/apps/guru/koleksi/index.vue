<template>
	<div class="grey lighten-4 fill-height mb-16">
		<div class="primary pb-16">
			<v-container>
				<Head
					title="Koleksi"
					subtitle="Kelola Koleksi Soal">
					<div>
						<v-btn
							small
							class="white"
							@click="dialog=true">
							<v-icon left>
								mdi-plus
							</v-icon>
							Tambah koleksi
						</v-btn>
						<v-btn
							small
							class="white"
							exact
							to="/apps/guru">
							<v-icon left>
								mdi-chevron-left
							</v-icon>
							Kembali
						</v-btn>
					</div>
				</Head>
			</v-container>
		</div>
		<v-container class="mt-n16">
			<v-card>
				<v-simple-table dense>
					<template
						v-slot:default>
						<thead>
							<tr>
								<th width="20">#</th>
								<th>Nama Koleksi</th>
								<th width="100">Jumlah Soal</th>
								<th width="100">Visibilitas</th>
								<th width="130">Dibuat</th>
								<th width="130"></th>
							</tr>
						</thead>
						<tbody>
							<tr
                                v-for="(item, index) in data"
                                :key="index">
								<td align="center">{{ index+1 }}</td>
								<td>{{ item.nama }}</td>
								<td align="center">{{ item.jumlah_soal}}</td>
								<td align="center">
                                    <v-chip v-if="item.visibilitas==1" class="primary" small>Publik</v-chip>
                                    <v-chip v-else class="danger" small>Private</v-chip>
                                </td>
								<td align="center">{{ $moment(item.dibuat).format('ll') }}</td>
								<td>
									<v-btn
                                        @click="handelHapusKoleksi(item.id)"
                                        small
                                        icon>
										<v-icon>mdi-delete</v-icon>
									</v-btn>
									<v-btn
                                        @click="handelEditKoleksi(item)"
                                        small
                                        icon>
										<v-icon>mdi-pencil</v-icon>
									</v-btn>
									<v-btn
                                        :to="`/apps/guru/koleksi/${item.id}`"
                                        small
                                        icon>
										<v-icon>mdi-eye</v-icon>
									</v-btn>
								</td>
							</tr>
						</tbody>
					</template>
				</v-simple-table>
			</v-card>
		</v-container>

		<v-dialog
			v-model="dialog"
			persistent
			max-width="600px">
			<v-card class="p-2">
				<v-card-title>Buat koleksi soal</v-card-title>
				<v-card-text>
					<v-text-field
						v-model="form.nama"
						dense
						label="Nama Koleksi"
						outlined
						required/>
                    <v-radio-group v-model="form.visibilitas" label="Visibilitas">
                        <v-radio
                            label="Private"
                            :value="0"/>
                        <v-radio
                            label="Publik"
                            :value="1"/>
                    </v-radio-group>
				</v-card-text>
				<v-card-actions>
					<v-spacer></v-spacer>
					<v-btn
						text
						@click="dialog = false">
						Batal
					</v-btn>
					<v-btn
						text
						@click="handelSimpanForm"
						outlined>
						Simpan
					</v-btn>
				</v-card-actions>
			</v-card>
		</v-dialog>


	</div>
</template>
<script>
export default {
	layout:'apps',
	props: [ 'setConfirmation', 'setSnackbar', 'setFetching' ],
	data: function(){

		return {
            dialog: false,
            data: [],
			form :{}
		}
	},
	mounted: function(){

        this.handelLoadData()
        this.handelResetForm()
    },
	methods:{

        handelLoadData: async function(){
            this.data   = (await this.$api(`/ujian/koleksi`)).data.data
        },

		handelResetForm: function(){
            this.form   = {
                nama: '',
                visibilitas: 0
            }
        },

		handelSimpanForm: function(){

            this.setFetching(true)

            if(this.form.id){

                this.$api.$put(`/ujian/koleksi/${this.form.id}`, this.form).then((resp)=>{
                    this.setSnackbar('Koleksi berhasil disimpan')
                    this.setFetching(false)
                    this.handelResetForm()
                    this.handelLoadData()
                    this.dialog = false
                })
            }else{

                this.$api.$post(`/ujian/koleksi`, this.form).then((resp)=>{
                    this.setSnackbar('Koleksi berhasil disimpan')
                    this.setFetching(false)
                    this.handelResetForm()
                    this.handelLoadData()
                    this.dialog = false
                })
            }


		},

		handelEditKoleksi: function(item){

            this.form   = Object.assign({}, item)
            this.dialog = true
		},

		handelHapusKoleksi: function(id){
			this.setConfirmation({
				status: true,
				title: 'Hapus ?',
				message: "Apakah anda yakin ingin menghapus koleksi ini ?",
				handelOk: ()=>{
					this.$api.$delete(`/ujian/koleksi/${id}`).then((resp)=>{
                        this.setSnackbar('Koleksi berhasil dihapus')
                        this.setFetching(false)
                        this.handelLoadData()
                    })
				}
			})
		}
	}
}
</script>
