<template>
	<div>
		<Head
			title="IDISI"
			subtitle="Sistem Informasi Akademik Terpadu"
			color="text--black"/>
		<v-row class="mt-6">
			<v-col v-for="(item, index) in apps[tipe]" :key="index" sm="12" md="3" cols="12">
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
	layout:'apps',
	data: () => ({
		tipe: 'calon',
		apps:{
			'admin': [
				{
					"ikon": "mdi-account-supervisor-circle",
					"nama":"PPDB",
					"deskripsi":"Sistem Pengelolaan Penerimaan Peserta Didik Baru",
					"link":"/apps/ppdb/beranda"
				},
				{
					"ikon": "mdi-school",
					"nama":"Akademik",
					"deskripsi":"Sistem Pengelolaan Data Akademik Terpadu",
					"link":"/apps/akademik/beranda"
				},
				{
					"ikon": "mdi-cash-multiple",
					"nama":"Keuangan",
					"deskripsi":"Sistem Pengelolaan Data Keuangan Terpadu",
					"link":"/apps/keuangan/beranda"
				},
				{
					"ikon": "mdi-family-tree",
					"nama":"Kepegawaian",
					"deskripsi":"Sistem Pengelolaan Data Kepegawaian Terpadu",
					"link":"/apps/kepegawaian/beranda"
				},
				{
					"ikon": "mdi-animation-play",
					"nama":"LMS",
					"deskripsi":"Learning Mangement System untuk Sekolah, Kurikulum, Ortu dan Siswa",
					"link":"lms",
					"link":"/apps/lms/beranda"
				},
			],
			'calon': [
				{
					"ikon": "mdi-account-supervisor-circle",
					"nama":"PPDB",
					"deskripsi":"Pendaftaran Peserta Didik Baru (Siswa Baru)",
					"link":"/apps/formulir"
				},
				{
					"ikon": "mdi-school",
					"nama":"Sekolah",
					"deskripsi":"Informasi Sekolah yang menerima pendaftaran peserta didik baru",
					"link":"/apps/akademik/beranda"
				},
			]
		}
    }),
	methods:{
		
	}
}
</script>
