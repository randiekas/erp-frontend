<template>
	<div class="grey lighten-4 fill-height mb-16">
		<div class="primary pb-16">
			<v-container>
				<Head
					title="Kelompok"
					subtitle="Detil kelompok rpl 1 ujian semester genap">
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
						<v-tab>Peserta Kuis</v-tab>
						<v-tab>Hasil Ujian</v-tab>
					</v-tabs>
				</v-col>
				<template v-if="tabActive===0">
					<v-col md="12">
						<v-card outlined>
							<v-simple-table dense>
								<template 
									v-slot:default>
									<thead>
										<tr>
											<th width="20">#</th>
											<th width="200">Email</th>
											<th>Nama</th>
											<th width="130"></th>
										</tr>
									</thead>
									<tbody>
										<tr>
											<td>1</td>
											<td>randiekas@gmail.com</td>
											<td>randi eka setiawan</td>
											<td>
												<v-btn @click="handelHapusKoleksi" small>
													Terima
												</v-btn>
											</td>
										</tr>
									</tbody>
								</template>
							</v-simple-table>
						</v-card>
					</v-col>
				</template>
				<template v-if="tabActive===1">
					<v-col md="12">
						<v-card outlined>
							<v-simple-table dense>
								<template 
									v-slot:default>
									<thead>
										<tr>
											<th width="20">#</th>
											<th width="200">Email</th>
											<th>Nama</th>
											<th width="130">Jumlah Benar</th>
											<th width="130">Jumlah Salah</th>
											<th width="130">Tidak Diisi</th>
											<th width="100"></th>
										</tr>
									</thead>
									<tbody>
										<tr>
											<td>1</td>
											<td>randiekas@gmail.com</td>
											<td>Randi Eka Setiawan</td>
											<td>8</td>
											<td>1</td>
											<td>1</td>
											<td>
												<v-btn @click="handelHapusKoleksi" small>
													Detil
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
