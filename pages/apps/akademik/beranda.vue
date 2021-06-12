<template>
	<div>
		<!-- <Head 
			title="Dashboard" 
			subtitle="Statistik Penerimaan Peserta Didik Baru"/> -->
		<Head
			title="Akademik"
			subtitle="Module kelola data akademik"
			color="text--black"/>
		<v-row justify="center" >
			<CardStats 
				sm="12" 
				md="3"
				title="Total Siswa Aktif" 
				:value="detil.total_pengunjung"/>
			<CardStats 
				sm="12" 
				md="3"
				title="Total Guru Tetap" 
				:value="detil.total_pendaftar"/>
			<CardStats 
				sm="12" 
				md="3"
				title="Total Guru Honorer" 
				:value="detil.total_penerimaan"/>
			<CardStats 
				sm="12" 
				md="3"
				title="Total Kelas" 
				:value="detil.total_penerimaan"/>
				
		</v-row>
		<Head 
			title="Modul" 
			subtitle="Berikut sub modul untuk kelola data akademik"
			color="text--black"/>
			
		<v-row>
			<v-col v-for="(item, index) in menu" :key="index" sm="12" md="3" cols="12">
				<v-card class="border--primary">
					<v-card-title class="pb-0">
						<v-icon left>{{item.ikon}}</v-icon>
						{{item.nama}}
					</v-card-title>
					<v-card-text>
						<div>{{item.deskripsi}}</div>
					</v-card-text>
					<v-card-actions>
						<v-spacer></v-spacer>
						<v-btn color="primary" text :to="item.link">
							Buka
							<v-icon right dark>mdi-launch</v-icon>
						</v-btn>
					</v-card-actions>
				</v-card>
			</v-col>
		</v-row>
		
	</div>
</template>
<script>
export default {
	async asyncData({ $api }) {
		let detil = (await $api.$get(`/api/v1/ppdb/dasbor/data`)).data
		return {
			detil
		}
	},
	data: ()=>({
		instruksiAktif:1,
		menu: [
				{
					"ikon": "mdi-account-group",
					"nama":"Kelas",
					"deskripsi":"Sistem Pengelolaan Kelas",
					"link":"/apps/akademik/kelas"
				},
				{
					"ikon": "mdi-account-supervisor-circle",
					"nama":"Siswa",
					"deskripsi":"Sistem Pengelolaan Siswa",
					"link":"/apps/akademik/siswa"
				},
				{
					"ikon": "mdi-account-tie",
					"nama":"Guru",
					"deskripsi":"Kelola Data Guru",
					"link":"/apps/akademik/guru"
				},
				{
					"ikon": "mdi-book-open-variant",
					"nama":"Pembelajaran",
					"deskripsi":"Kelola Data Pembelajaran",
					"link":"/apps/akademik/pembelajaran"
				},
				{
					"ikon": "mdi-calendar-clock",
					"nama":"Jadwal",
					"deskripsi":"Kelola Data Jadwal",
					"link":"/apps/akademik/jadwal"
				},
				{
					"ikon": "mdi-chart-box",
					"nama":"Raport",
					"deskripsi":"Kelola Data Raport",
					"link":"/apps/akademik/raport"
				}
				
		],
	})
}
</script>