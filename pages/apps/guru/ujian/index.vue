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
								<th width="130">Dibuat</th>
								<th width="130"></th>
							</tr>
						</thead>
						<tbody>
							<tr>
								<td>1</td>
								<td>Ujian PAS</td>
								<td>2</td>
								<td>20</td>
								<td>30 Menit</td>
								<td>20 juni 2021</td>
								<td>
									<v-btn @click="handelHapusKoleksi" small icon>
										<v-icon>mdi-delete</v-icon>
									</v-btn>
									<v-btn small icon>
										<v-icon>mdi-pencil</v-icon>
									</v-btn>
									<v-btn to="/apps/guru/ujian/1" small icon>
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
	props: ['setConfirmation'],
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
				nama: '',
				durasi: 30
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
                nama: '',
				durasi: 30
            }
        },
		handelSimpanForm: function(){

		},
		handelHapusKoleksi: function(){
			this.setConfirmation({
				status: true,
				title: 'Hapus ?',
				message: "Apakah anda yakin ingin menghapus koleksi ini ?",
				handelOk: ()=>{
					// this.setConfirmation({ status: false })
				}
			})
		}
	}
}
</script>
