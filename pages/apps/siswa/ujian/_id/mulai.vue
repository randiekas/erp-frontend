<template>
	<div class="grey lighten-4 fill-height mb-16">
		<div class="primary pb-16">
			<v-container>
				<Head
					title="Ujian"
					subtitle="Selamat Mengerjakan Ujian">
					<v-card outlined rounded="lg">
						<v-card-text>
							<p class="text-h3 black--text mb-0">09:00</p>
						</v-card-text>
					</v-card>
				</Head>
			</v-container>
		</div>
		<v-container class="mt-n16">
			<v-card
				class="mb-4">

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
										class="success"
										rounded="lg">
										Selesai
									</v-btn>
								</v-card-text>
							</v-card>
						</div>
						<v-divider class="m-0 p-0"/>
						<v-row class="mt-0">
							<v-col class="text-center px-4 d-flex" style="align-items:center">
								<span v-if="ujian.status" class="black--text text-h4">{{ ujian.nilai }}</span>
								<v-btn v-else outlined>Belum dijawab: 20</v-btn>
							</v-col>
							<v-col class="text-center">
								<my-text
									title="Jumlah Soal"
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
			<v-row dense>
				<v-col md="8">
					<p class="text-overline mb-0">Soal 1</p>
					<v-card outlined class="mb-2">
						<v-card-text>
							<p class="mb-0">Ibu mempunyai sebuah kue. Kue tersebut dipotong menjadi 4 bagian sama besar. Satu potong diberikan kepada adik. Adik menerima kue sebanyak . . . .</p>
						</v-card-text>
					</v-card>
					<p class="text-overline mb-0">Jawaban kamu</p>
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
				</v-col>
				<v-col md="4">
					<p class="text-overline mb-0">Nomor soal</p>
					<v-card outlined>
						<v-card-text>
							<v-row justify="space-between" dense>
								<v-col 
									v-for="item in [1,2,3,4,5,6,7,8,9,10]"
									:key="item">
									<v-btn 
										small
										outlined>{{ item }}</v-btn>
								</v-col>
							</v-row>
						</v-card-text>
					</v-card>
				</v-col>
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
			tipe
		}
	},
	data: function(){
		return {
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
			peserta: [
				{
					lokasi: 'https://lh3.googleusercontent.com/a-/AOh14Gi4xaqxMKNwVPnZoD16EBOJZXF-6VMZSUn3PF8FNg=s96-c',
					nama: 'Randi eka setiawan',
					nilai: '-',
				},
				{
					lokasi: 'https://lh3.googleusercontent.com/a-/AOh14Gi4xaqxMKNwVPnZoD16EBOJZXF-6VMZSUn3PF8FNg=s96-c',
					nama: 'Randi eka setiawan',
					nilai: '-',
				},
				{
					lokasi: 'https://lh3.googleusercontent.com/a-/AOh14Gi4xaqxMKNwVPnZoD16EBOJZXF-6VMZSUn3PF8FNg=s96-c',
					nama: 'Randi eka setiawan',
					nilai: '-',
				},
				{
					lokasi: 'https://lh3.googleusercontent.com/a-/AOh14Gi4xaqxMKNwVPnZoD16EBOJZXF-6VMZSUn3PF8FNg=s96-c',
					nama: 'Randi eka setiawan',
					nilai: '-',
				},
				{
					lokasi: 'https://lh3.googleusercontent.com/a-/AOh14Gi4xaqxMKNwVPnZoD16EBOJZXF-6VMZSUn3PF8FNg=s96-c',
					nama: 'Randi eka setiawan',
					nilai: '-',
				},
				{
					lokasi: 'https://lh3.googleusercontent.com/a-/AOh14Gi4xaqxMKNwVPnZoD16EBOJZXF-6VMZSUn3PF8FNg=s96-c',
					nama: 'Randi eka setiawan',
					nilai: '-',
				},
				{
					lokasi: 'https://lh3.googleusercontent.com/a-/AOh14Gi4xaqxMKNwVPnZoD16EBOJZXF-6VMZSUn3PF8FNg=s96-c',
					nama: 'Randi eka setiawan',
					nilai: '-',
				},
				{
					lokasi: 'https://lh3.googleusercontent.com/a-/AOh14Gi4xaqxMKNwVPnZoD16EBOJZXF-6VMZSUn3PF8FNg=s96-c',
					nama: 'Randi eka setiawan',
					nilai: '-',
				},
				{
					lokasi: 'https://lh3.googleusercontent.com/a-/AOh14Gi4xaqxMKNwVPnZoD16EBOJZXF-6VMZSUn3PF8FNg=s96-c',
					nama: 'Randi eka setiawan',
					nilai: '-',
				},
				{
					lokasi: 'https://lh3.googleusercontent.com/a-/AOh14Gi4xaqxMKNwVPnZoD16EBOJZXF-6VMZSUn3PF8FNg=s96-c',
					nama: 'Randi eka setiawan',
					nilai: '-',
				}
			]
		}
	},
	methods:{
		
	}
}
</script>
