<template>
	<div class="grey lighten-4 fill-height mb-16">
		<div class="primary pb-16">
			<v-container>
				<Head
					title="Detil"
					:subtitle="detail.nama">
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
							@click="handelResetForm">
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
		<v-container
            v-if="detail.id"
            class="mt-n16">
			<v-row dense>
				<v-col md="8">
					<v-card outlined class="mb-2">
						<v-card-title v-if="form.id">Soal {{ current }}</v-card-title>
						<v-card-title v-else>Form Tambah Soal</v-card-title>
						<v-card-text>
							<div class="mb-4">
								<p class="text-overline mb-0 black--text">Level Soal</p>
								<v-row>
									<v-col
                                        v-for="(item, index) in ['beginner', 'easy', 'normal', 'hard', 'very hard']"
                                        :key="index">
										<v-card
											outlined
											hover
                                            :class="form.level===index?'border--primary':''"
                                            @click="form.level=index">
											<v-card-text class="text-center">
												<v-icon
                                                    :class="form.level===index?'primary--text':''"
                                                    size="42">mdi-folder-text-outline</v-icon>
                                                    <p class="text-overline  mb-0">{{ item }}</p>
											</v-card-text>
										</v-card>
									</v-col>

								</v-row>
							</div>
							<v-divider class="mb-4"/>
							<div class="mb-4">
								<p class="text-overline mb-0 black--text">Tipe Soal</p>
								<v-row>
									<v-col
                                        v-for="(item, index) in ['pilihan ganda', 'benar salah', 'isian', 'essay']"
                                        :key="index">
										<v-card
											outlined
											hover
                                            :class="form.tipe===index?'border--primary':''"
                                            @click="form.tipe=index">
											<v-card-text class="text-center">
												<v-icon
                                                    :class="form.tipe===index?'primary--text':''"
                                                    size="42">mdi-folder-text-outline</v-icon>
                                                    <p class="text-overline  mb-0">{{ item }}</p>
											</v-card-text>
										</v-card>
									</v-col>

								</v-row>
							</div>
							<v-divider class="mb-4"/>
							<div class="mb-4">
								<p class="text-overline mb-0 black--text">Pertanyaan</p>
                                <my-editor v-model="form.pertanyaan"/>
							</div>
							<v-divider class="mb-4"/>
							<div class="mb-4">
								<p class="text-overline mb-0 black--text">Opsi Jawaban</p>
								
								<div 
									v-for="(item, index) in form.opsi"
									:key="index"
									outlined 
									class="d-flex py-2 align-items-center" 
									style="align-items: center">

									<v-avatar size="30" class="primary white--text mr-4">
										<b>{{ indexAlphabet[index] }}</b>
									</v-avatar>
									<v-text-field
										dense
										v-model="form.opsi[index]"
										hide-details=""
										class="w-100"/>

								</div>
							</div>
							<v-divider class="mb-4"/>
							<div class="mb-4">
								<p class="text-overline black--text">Jawaban Benar</p>
								<v-row>
									<v-col 
										v-for="(item, index) in form.opsi.length"
										:key="index"
										style="text-align: center">
										<v-btn 
											@click="form.jawaban=index"
											outlined
											:class="index==form.jawaban?'primary white--text border--primary':''">
											{{ indexAlphabet[index] }}
										</v-btn>
									</v-col>
								</v-row>

							</div>
						</v-card-text>
						<v-card-actions>
							<v-spacer></v-spacer>
							<v-btn
								text
								@click="handelResetForm">
								Reset
							</v-btn>
							<v-btn
								v-if="form.id"
								outlined
								text
								@click="handelHapus">
								<v-icon icon>mdi-delete</v-icon>
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
                            <v-alert
                                v-if="detail.soal.length==0"
                                type="info"
                                dense>
                                    Belum ada soal yang dibuat
                            </v-alert>
							<v-row
                                v-else
								justify="space-between"
                                dense>
								<v-col
									v-for="item in detail.soal.length"
									@click="handelPilihSoal(item)"
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
	props: [ 'setConfirmation', 'setSnackbar', 'setFetching' ],
    async asyncData({ params }) {

        return {
            id: params.id
        }
    },
	data: function(){

		return {
            detail: {
                soal: [],
            },
			form :{},
			current: 0,
		}
	},
	mounted: function(){

        this.handelLoadData()
        this.handelResetForm()
        // this.handelLoadDataPelajaran()
    },
	methods:{

        handelLoadData: async function(){

            this.detail     = (await this.$api(`/ujian/koleksi/${this.id}`)).data.data
        },

		handelPilihSoal(index){

			let item 		= Object.assign({}, this.detail.soal[index-1])
			item.opsi		= JSON.parse(item.opsi)
			this.current	= index
			this.form		= item
		},

		handelResetForm: function(){

            this.form   = {
                level: 0,
                tipe: 0,
                pertanyaan: '',
                opsi: ['','','','',''],
                jawaban: 0
            }
        },

		handelSimpanForm: function(){

			this.setFetching(true)

			let payload		= Object.assign({}, this.form)
			payload.opsi	= JSON.stringify(payload.opsi)
			this.$api.$post(`/ujian/koleksi/${this.id}/soal`, payload).then((resp)=>{
				this.setSnackbar('Soal berhasil ditambahkan')
				this.setFetching(false)
				this.handelResetForm()
				this.handelLoadData()
				this.dialog = false
			})
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
