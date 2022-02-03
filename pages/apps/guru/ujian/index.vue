<template>
	<div class="grey lighten-4 fill-height mb-16">
		<div class="primary pb-16">
			<v-container>
				<Head
					title="Ujian"
					subtitle="Kelola Koleksi Ujian">
					<div>
						<v-btn
							small
							class="white"
							@click="dialog=true">
							<v-icon left>
								mdi-plus
							</v-icon>
							Tambah Ujian
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
								<th>Nama Ujian</th>
								<th width="130">Jumlah Batch</th>
								<th width="130">Jumlah Soal</th>
								<th width="130">Durasi Ujian</th>
								<th width="250">Berbatas waktu</th>
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
								<td align="center">{{ item.jumlah_kelompok }}</td>
								<td align="center">{{ item.jumlah_soal }}</td>
								<td align="center">{{ item.durasi }} Menit</td>
								<td align="center">
                                    <div v-if="item.terjadwal">
                                        {{ $moment(item.dimulai).format('DD MMM (hh:mm)') }} - {{ $moment(item.selesai).format('DD MMM (hh:mm)') }}
                                    </div>
                                    <div v-else>-</div>
                                </td>
                                <td align="center">{{ $moment(item.dibuat).format('ll') }}</td>
								<td>
									<v-btn
                                        @click="handelHapus(item.id)"
                                        small
                                        icon>
										<v-icon>mdi-delete</v-icon>
									</v-btn>
									<v-btn
                                        @click="handelEdit(item)"
                                        small
                                        icon>
										<v-icon>mdi-pencil</v-icon>
									</v-btn>
									<v-btn
                                        :to="`/apps/guru/ujian/${item.id}`"
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
				<v-card-title>Buat Ujian</v-card-title>
				<v-card-text>
					<v-text-field
						v-model="form.nama"
						dense
						label="Nama Ujian"
						outlined
						required/>
					<v-text-field
						type="number"
						v-model="form.durasi"
						dense
						label="Durasi (menit)"
						outlined
						required/>

                    <div class="d-flex justify-space-between">
                        <p>Berbatas Waktu ?</p>
                        <v-switch
                            class="mt-0"
                            dense
                            v-model="form.terjadwal"/>
                    </div>
                    <template v-if="form.terjadwal">
						
                        <v-text-field
                            type="datetime-local"
                            v-model="form.mulai"
                            dense
                            label="Mulai dapat diakses pada"
                            outlined
                            required/>

                        <v-text-field
                            type="datetime-local"
                            v-model="form.berakhir"
                            dense
                            label="Selesai dapat diakses pada"
                            outlined
                            required/>
                    </template>
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
			form :{
				nama: '',
				durasi: 30
			}
		}
	},
	mounted: function(){
        this.handelLoadData()
        // this.handelLoadDataPelajaran()
        // this.handelResetForm()
    },
	methods:{

        handelLoadData: async function(){

            this.data   = (await this.$api(`/ujian`)).data.data
        },

		handelResetForm: function(){
            this.form   = {
                nama: '',
				durasi: 30,
				terjadwal: 0,
            }
        },

		handelSimpanForm: function(){

            this.setFetching(true)

            this.form.terjadwal = this.form.terjadwal?true:false
            if(this.form.id){

                this.$api.$put(`/ujian/${this.form.id}`, this.form).then((resp)=>{
                    this.setSnackbar('Ujian berhasil diubah')
                    this.setFetching(false)
                    this.handelResetForm()
                    this.handelLoadData()
                    this.dialog = false
                })
            }else{

                this.$api.$post(`/ujian`, this.form).then((resp)=>{
                    this.setSnackbar('Ujian berhasil ditambahkan')
                    this.setFetching(false)
                    this.handelResetForm()
                    this.handelLoadData()
                    this.dialog = false
                })
            }
		},

		handelEdit: function(item){

            this.form   = Object.assign({}, item)
            this.dialog = true
		},

		handelHapus: function(id){

			this.setConfirmation({
				status: true,
				title: 'Hapus ?',
				message: "Apakah anda yakin ingin menghapus ujian ini ?",
				handelOk: ()=>{
					this.$api.$delete(`/ujian/${id}`).then((resp)=>{
                        this.setSnackbar('Ujian berhasil dihapus')
                        this.setFetching(false)
                        this.handelLoadData()
                    })
				}
			})
		}
	}
}
</script>
