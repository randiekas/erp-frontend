<template>
	<div class="grey lighten-4 fill-height mb-16">
		<div class="primary pb-16">
			<v-container>
				<Head
					title="Detail"
					subtitle="Kelola detail ujian">
					<div>
						<v-btn
							small
							class="white"
							exact
							to="/apps/guru/ujian">
							<v-icon left>
								mdi-chevron-left
							</v-icon>
							Kembali
						</v-btn>
					</div>
				</Head>
			</v-container>
		</div>
		<v-container 
			v-if="detail.id"
			class="mt-n16">
			<v-row dense>
				<v-col md="12">
					<v-card
						class="mb-2">

						<v-card-text class="d-flex">
							<div class="flex-grow-1 fill-width">
								<div class="d-flex justify-space-between align-center">
									<div>
										<v-card-title class="black--text text-truncate">{{ detail.nama }}</v-card-title>
										<v-card-subtitle>Detail Ujian</v-card-subtitle>
									</div>
									<v-card outlined rounded="lg">
										<v-card-text>
											<v-btn
												small
												:to="`/apps/siswa/ujian/${ujian.id}/mulai`"
												class="primary"
												rounded="lg">
												Monitoring Realtime
											</v-btn>
										</v-card-text>
									</v-card>
								</div>
								<v-divider class="m-0 p-0"/>
								<v-row class="mt-0">
									<v-col class="text-center px-4">
										<span v-if="ujian.status" class="black--text text-h4">{{ ujian.nilai }}</span>
										<v-btn v-else outlined>Belum Selesai</v-btn>
									</v-col>
									<v-col class="text-center">
										<my-text
											title="Jumlah batch"
											:subtitle="ujian.jumlah_peserta||'-'"
											/>
									</v-col>
									<v-col class="text-center">
										<my-text
											title="Jumlah peserta"
											:subtitle="ujian.jumlah_peserta||'-'"
											/>
									</v-col>
									<v-col class="text-center">
										<my-text
											title="Durasi Ujian"
											:subtitle="ujian.durasi||'-'"/>
									</v-col>
									<v-col class="text-center">
										<my-text
											title="Mulai ujian"
											:subtitle="ujian.mulai_ujian||'-'"/>
									</v-col>
									<v-col class="text-center">
										<my-text
											title="Berakhir Ujian"
											:subtitle="ujian.berakhir_ujian||'-'"
											/>
									</v-col>
								</v-row>
							</div>
						</v-card-text>
					</v-card>
				</v-col>
				<v-col md="12">
					<v-tabs v-model="tabActive">
						<v-tab>Kelola Soal</v-tab>
						<v-tab>Kelola Kelompok Peserta Ujian</v-tab>
					</v-tabs>
				</v-col>
				<template v-if="tabActive===0">
					<v-col md="8">
						<v-card outlined class="mb-2">
							<v-card-title>Soal 1</v-card-title>
							<v-card-text>
								<div class="mb-4">
									<p class="text-overline mb-0 black--text">Level Soal</p>
									<v-row>
										<v-col>
											<v-card 
												outlined 
												hover>
												<v-card-text class="text-center">
													<v-icon class="black--text" size="42">mdi-folder-text-outline</v-icon>
													<p class="text-overline  mb-0">Beginner</p>
												</v-card-text>
											</v-card>
										</v-col>
										<v-col>
											<v-card 
												outlined 
												hover>
												<v-card-text class="text-center">
													<v-icon class="black--text" size="42">mdi-folder-text-outline</v-icon>
													<p class="text-overline  mb-0">Easy</p>
												</v-card-text>
											</v-card>
										</v-col>
										<v-col>
											<v-card 
												outlined 
												hover>
												<v-card-text class="text-center">
													<v-icon class="black--text" size="42">mdi-folder-text-outline</v-icon>
													<p class="text-overline  mb-0">Normal</p>
												</v-card-text>
											</v-card>
										</v-col>
										<v-col>
											<v-card 
												outlined 
												hover>
												<v-card-text class="text-center">
													<v-icon class="black--text" size="42">mdi-folder-text-outline</v-icon>
													<p class="text-overline  mb-0">Hard</p>
												</v-card-text>
											</v-card>
										</v-col>
										<v-col>
											<v-card 
												outlined 
												hover>
												<v-card-text class="text-center">
													<v-icon class="black--text" size="42">mdi-folder-text-outline</v-icon>
													<p class="text-overline  mb-0">Very Hard</p>
												</v-card-text>
											</v-card>
										</v-col>
									</v-row>
								</div>
								<v-divider class="mb-4"/>
								<div class="mb-4">
									<p class="text-overline mb-0 black--text">Tipe Soal</p>
									<v-row>
										<v-col>
											<v-card 
												outlined 
												hover>
												<v-card-text class="text-center">
													<v-icon class="black--text" size="42">mdi-folder-text-outline</v-icon>
													<p class="text-overline  mb-0">Pilihan Ganda</p>
												</v-card-text>
											</v-card>
										</v-col>
										<v-col>
											<v-card 
												outlined 
												hover>
												<v-card-text class="text-center">
													<v-icon class="black--text" size="42">mdi-folder-text-outline</v-icon>
													<p class="text-overline  mb-0">Benar Salah</p>
												</v-card-text>
											</v-card>
										</v-col>
										<v-col>
											<v-card 
												outlined 
												hover>
												<v-card-text class="text-center">
													<v-icon class="black--text" size="42">mdi-folder-text-outline</v-icon>
													<p class="text-overline  mb-0">Isian</p>
												</v-card-text>
											</v-card>
										</v-col>
										<v-col>
											<v-card 
												outlined 
												hover>
												<v-card-text class="text-center">
													<v-icon class="black--text" size="42">mdi-folder-text-outline</v-icon>
													<p class="text-overline  mb-0">Essay</p>
												</v-card-text>
											</v-card>
										</v-col>
									</v-row>
								</div>
								<v-divider class="mb-4"/>
								<div class="mb-4">
									<p class="text-overline mb-0 black--text">Pertanyaan</p>
									<p class="mb-0">Ibu mempunyai sebuah kue. Kue tersebut dipotong menjadi 4 bagian sama besar. Satu potong diberikan kepada adik. Adik menerima kue sebanyak . . . .</p>
								</div>
								<v-divider class="mb-4"/>
								<div class="mb-4">
									<p class="text-overline mb-0 black--text">Opsi Jawaban</p>
									<v-card outlined hover class="mb-2">
										<v-card-text class="d-flex py-2 align-items-center" style="align-items: center">
											<v-avatar size="30" class="primary white--text mr-4"><b>A</b></v-avatar>
											<div class="text-align-center justify-content-center">
												Setengah bagian
											</div>
										</v-card-text>
									</v-card>
									<v-card outlined hover class="mb-2">
										<v-card-text class="d-flex py-2 align-items-center" style="align-items: center">
											<v-avatar size="30" class="primary white--text mr-4"><b>B</b></v-avatar>
											<div class="text-align-center justify-content-center">
												Setengah bagian
											</div>
										</v-card-text>
									</v-card>
									<v-card outlined hover class="mb-2">
										<v-card-text class="d-flex py-2 align-items-center" style="align-items: center">
											<v-avatar size="30" class="primary white--text mr-4"><b>C</b></v-avatar>
											<div class="text-align-center justify-content-center">
												Setengah bagian
											</div>
										</v-card-text>
									</v-card>
								</div>
								<v-divider class="mb-4"/>
								<div class="mb-4">
									<p class="text-overline mb-0 black--text">Jawaban Benar</p>
									<v-row>
										<v-col>
											<v-card outlined hover class="mb-2">
												<v-card-text class="d-flex py-2 align-items-center" style="align-items: center">
													<v-avatar size="30" class="primary white--text mr-4"><b>A</b></v-avatar>
												</v-card-text>
											</v-card>
										</v-col>
										<v-col>
											<v-card outlined hover class="mb-2">
												<v-card-text class="d-flex py-2 align-items-center" style="align-items: center">
													<v-avatar size="30" class="primary white--text mr-4"><b>A</b></v-avatar>
												</v-card-text>
											</v-card>
										</v-col>
										<v-col>
											<v-card outlined hover class="mb-2">
												<v-card-text class="d-flex py-2 align-items-center" style="align-items: center">
													<v-avatar size="30" class="primary white--text mr-4"><b>C</b></v-avatar>
												</v-card-text>
											</v-card>
										</v-col>
									</v-row>
									
								</div>
							</v-card-text>
							<v-card-actions>
								<v-spacer></v-spacer>
								<v-btn
									text
									@click="handelSimpanForm"
									outlined>
									Hapus Soal
								</v-btn>
							</v-card-actions>
						</v-card>
						
						
					</v-col>
					<v-col md="4">
						<v-card outlined>
					
							<v-card-text>
								<p class="text-overline black--text">Nomor Soal</p>
								<v-row justify="space-between" dense>
									<v-col 
										v-for="item in [1,2,3,4,5,6,7,8,9,10]"
										:key="item"
										class="text-center">
										<v-btn 
											small
											outlined>{{ item }}</v-btn>
									</v-col>
								</v-row>
								<v-btn 
									class="primary mt-4" 
									block 
									small>
									<v-icon left>
										mdi-upload
									</v-icon>
									Import Soal
								</v-btn>
							</v-card-text>
							
						</v-card>
					</v-col>
				</template>
				<template v-if="tabActive===1">
					<v-col md="12">
						<div class="text-right mb-4">
							<v-btn 
								small
								class="primary"
								@click="dialog=true">
								Tambah Kelompok peserta
							</v-btn>
						</div>
						<v-card outlined>
							<v-simple-table dense>
								<template 
									v-slot:default>
									<thead>
										<tr>
											<th width="20">#</th>
											<th>Nama Kelompok</th>
											<th width="130">Kode Ujian</th>
											<th width="100">Visibilitas</th>
											<th width="130">Jumlah Peserta</th>
											<th width="130">Dibuat</th>
											<th width="130"></th>
										</tr>
									</thead>
									<tbody>
										<tr
											v-for="(item, index) in detail.kelompok"
											:key="index">
											<td align="center">{{ index+1 }}</td>
											<td>{{ item.nama }}</td>
											<td>{{ item.uuid }}</td>
											<td align="center">
												<v-chip v-if="item.visibilitas==1" class="primary" small>Publik</v-chip>
												<v-chip v-else class="danger" small>Private</v-chip>
											</td>
											<td align="center">{{ item.jumlah_peserta }}</td>
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
													to="/apps/guru/ujian/1/kelompok/1"
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
					</v-col>
				</template>
			</v-row>
			<v-row dense>
				
				
			</v-row>
		</v-container>

		<!-- form kelompok -->
		<v-dialog
			v-model="dialog"
			persistent
			max-width="600px">
			<v-card class="p-2">
				<v-card-title>Buat Kelompok</v-card-title>
				<v-card-text>
					<v-text-field
						v-model="form.nama"
						dense
						label="Nama Kelompok"
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
    async asyncData({ params }) {

        return {
            id: params.id,
			ujian: {
				id: 1,
				lokasi: 'https://olle-tryout-new.sfo2.digitaloceanspaces.com/biibo/file_unggah/Add%20a%20subheading%20%288%29.jpg',
				nama: 'Ujian Tengah Semester',
				jumlah_peserta: 30,
				pelajaran: 'Matematika',
				mulai_ujian: '2021-12-06',
				berakhir_ujian: '2021-12-06',
				durasi: '30 menit',
				nilai: 80,
				status:0
			},
        }
    },
	data: function(){

		return {
            detail: {
                soal: [],
            },
			form :{},
			current: 0,
			tabActive: 0,
			dialog: false,
		}
	},
	mounted: function(){

        this.handelLoadData()
        this.handelResetForm()
        // this.handelLoadDataPelajaran()
    },
	
	methods:{
		handelLoadData: async function(){

            // this.soal     	= (await this.$api(`/ujian/${this.id}/soal`)).data.data
            this.detail     = (await this.$api(`/ujian/${this.id}`)).data.data
        },
		handelResetForm: function(){
            this.form   = {
                nama: '',
				visibilitas: 0
            }
        },
		handelSimpanForm: function(){

			this.setFetching(true)

			let payload		= Object.assign({}, this.form)

            if(payload.id){

                this.$api.$put(`/ujian/${this.id}/kelompok/${payload.id}`, payload).then((resp)=>{
                    this.setSnackbar('Kelompok berhasil diubah')
                    this.setFetching(false)
                    this.handelLoadData()
                    this.dialog = false
                })
            }else{

                this.$api.$post(`/ujian/${this.id}/kelompok`, payload).then((resp)=>{
                    this.setSnackbar('Kelompok berhasil ditambahkan')
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
				message: "Apakah anda yakin ingin menghapus soal ini ?",
				handelOk: ()=>{
					this.$api.$delete(`/ujian/koleksi/${this.id}/soal/${this.form.id}`).then((resp)=>{
                        this.setSnackbar('Soal berhasil dihapus')
                        this.setFetching(false)
						this.handelResetForm()
                        this.handelLoadData()
                    })
				}
			})
		}
	}
}
</script>
