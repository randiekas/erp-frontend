<template>
	<div class="grey lighten-4 fill-height mb-16">
		<div class="primary pb-16">
			<v-container>
				<Head
					title="Hello"
					subtitle="Selamat datang kembali di IDISI">
					<v-btn
						small
						class="white"
                        @click="handelKeluar">
						<v-icon left>
							mdi-logout
						</v-icon>
						Logout
					</v-btn>
				</Head>
			</v-container>
		</div>
		<v-container class="mt-n16">
			<v-card class="mb-4">
				<v-card-title>Kelola Ujian</v-card-title>
				<v-card-subtitle>Masukkan kode ujian untuk masuk kedalam ujian</v-card-subtitle>
				<v-card-text class="d-flex justify-center">
					<div class="flex-grow-1 mr-4">
						<v-text-field
							dense
							outlined
							label="Kode Ujian"
							hide-details=""/>
					</div>
					<v-btn rounded class="primary">Gabung</v-btn>
				</v-card-text>
			</v-card>
			<p class="text-overline">Daftar ujian kamu</p>
			<div
				v-for="(item, index) in ujian"
				:key="index">
				<my-list-ujian
					:item="item"/>
			</div>
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
			ujian:[
				{
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
				{
					id: 1,
					lokasi: 'https://olle-tryout-new.sfo2.digitaloceanspaces.com/biibo/file_unggah/Add%20a%20subheading%20%288%29.jpg',
					nama: 'Ujian Tengah Semester',
					jumlah_peserta: 30,
					pelajaran: 'Matematika',
					mulai_ujian: '2021-12-06',
					berakhir_ujian: '2021-12-06',
					durasi: '30 menit',
					nilai: 80,
					status:1
				}
			]
		}
	},
	methods:{
		
	}
}
</script>
