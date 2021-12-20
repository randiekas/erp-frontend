<template>
	<div class="grey lighten-4 fill-height mb-16">
		<div class="primary pb-16">
			<v-container>
				<Head
					title="Detil"
					subtitle="Koleksi soal un 2021">
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
		<v-container class="mt-n16">
			<v-row dense>
				<v-col md="12">
					<v-card
						class="mb-2">

						<v-card-text class="d-flex">
							<div class="flex-grow-1 fill-width">
								<div class="d-flex justify-space-between align-center">
									<div>
										<v-card-title class="black--text text-truncate">{{ ujian.nama }}</v-card-title>
										<v-card-subtitle>{{ ujian.pelajaran }}</v-card-subtitle>
									</div>
									<v-card outlined rounded="lg">
										<v-card-text>
											<v-btn
												small
												:to="`/apps/siswa/ujian/${ujian.id}/mulai`"
												class="primary"
												rounded="lg">
												Mulai Ujian
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
								class="primary">
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
											<th width="130">Jumlah Peserta</th>
											<th width="130">Dimulai</th>
											<th width="130">Selesai</th>
											<th width="130">Dibuat</th>
											<th width="130"></th>
										</tr>
									</thead>
									<tbody>
										<tr>
											<td>1</td>
											<td>Kelas Ipa 1</td>
											<td>Pqzsd30</td>
											<td>30</td>
											<td>20 juni 2021</td>
											<td>20 juni 2021</td>
											<td>20 juni 2021</td>
											<td>
												<v-btn @click="handelHapusKoleksi" small icon>
													<v-icon>mdi-delete</v-icon>
												</v-btn>
												<v-btn small icon>
													<v-icon>mdi-pencil</v-icon>
												</v-btn>
												<v-btn to="/apps/guru/ujian/1/kelompok/1" small icon>
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

	</div>
</template>
<script>
export default {
	layout:'apps',
	async asyncData({ $auth}) {
		const tipe			= $auth.$storage.getUniversal("loginType")
		return {
			tipe,
			dialog: false,
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
			tabActive: 0,
			form :{
				nama: ''
			}
		}
	},
	mounted: function(){
        // this.handelLoadData()
        // this.handelLoadDataPelajaran()
        // this.handelResetForm()
    },
	methods:{
		handelResetForm: function(){
            this.form   = {
                nama: ''
            }
        },
		handelSimpanForm: function(){

		}
	}
}
</script>
