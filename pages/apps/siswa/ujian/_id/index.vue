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
                        to="/apps/siswa"
						exact>
						<v-icon left>
							mdi-chevron-left
						</v-icon>
						Kembali
					</v-btn>
				</Head>
			</v-container>
		</div>
		<v-container class="mt-n16">
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
								<v-btn v-else outlined>Belum Mengerjakan</v-btn>
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
			<p class="text-overline">Peserta ujian</p>
			<v-row dense>
				<v-col 
					v-for="(item, index) in peserta"
					cols="12"
					md="4"
					:key="index">
					<v-card 
						dark 
						color="primary" >
						<v-list-item>
							<v-list-item-avatar>
								<v-avatar
									color="primary">
									<v-img :src="item.lokasi"/>
								</v-avatar>
							</v-list-item-avatar>
							<v-list-item-content>
								<v-list-item-title>{{ item.nama }}</v-list-item-title>
								<v-list-item-subtitle>{{ item.email }}</v-list-item-subtitle>
							</v-list-item-content>
							<v-list-item-action-text>
								{{ item.nilai }}
							</v-list-item-action-text>
						</v-list-item>
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
