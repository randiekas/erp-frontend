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
							@click="dialog=true">
							<v-icon left>
								mdi-upload
							</v-icon>
							Import Soal
						</v-btn>
						<v-btn
							small
							class="white"
							@click="dialog=true">
							<v-icon left>
								mdi-plus
							</v-icon>
							Tambah Soal
						</v-btn>
						<v-btn
							small
							class="white"
							exact
							to="/apps/guru/koleksi">
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
								@click="dialog = false">
								Reset
							</v-btn>
							<v-btn
								text
								@click="handelSimpanForm"
								outlined>
								Simpan
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
						</v-card-text>
						
					</v-card>
				</v-col>
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
		}
	},
	data: function(){
		return {
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
