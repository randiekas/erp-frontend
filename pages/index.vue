<template>
<div>
	<v-container class="my-16 py-16">
        <v-row justify="center" align="center">
            <v-col md="6">
				<p class="text-overline secondary--text">Welcome to IDISI</p>
                <h1 class="text-h1">Aplikasi<br/><span class="primary--text">Ujian</span> #1 </h1>
                <p class="mt-4 text-overline" style="font-size:11pt!important">Sudah digunakan oleh 100 sekolah serta lebih dari 20 ribu siswa</p>
				<v-btn @click="handelMasuk" rounded block class="primary">Mulai sekarang</v-btn>
            </v-col>
            <v-col md="6">
                <v-img
                    src="https://prod-notion-assets.s3-us-west-2.amazonaws.com/front/product/hero.png"/>
            </v-col>
        </v-row>
    </v-container>
	<div class="grey lighten-4">
		<v-container class="py-16">
			<h2 class="text-h3">Keunggulan IDISI</h2>
			<p class="mt-4">IDISI memiliki fitur-fitur lengkap yang diperlukan untuk ujian online</p>
			<v-row class="mt-4">
				<v-col md="3">
					<v-card outlined rounded="lg">
						<v-card-text class="pb-0">
							<v-icon size="64">mdi-account-sync-outline</v-icon>
						</v-card-text>
						<v-card-title>Status Online</v-card-title>
						<v-card-text>
							Di dashboard guru ada online offline peserta ujian
						</v-card-text>
					</v-card>
				</v-col>
				<v-col md="3">
					<v-card outlined rounded="lg">
						<v-card-text class="pb-0">
							<v-icon size="64">mdi-file-word-box</v-icon>
						</v-card-text>
						<v-card-title>Import Soal</v-card-title>
						<v-card-text>
							Soal dapat di import dari microsoft word
						</v-card-text>
					</v-card>
				</v-col>
				<v-col md="3">
					<v-card outlined rounded="lg">
						<v-card-text class="pb-0">
							<v-icon size="64">mdi-account-sync-outline</v-icon>
						</v-card-text>
						<v-card-title>Analisis Soal</v-card-title>
						<v-card-text>
							Tersedia laporan analisis butir soal, dan tingkat kesulitan soal
						</v-card-text>
					</v-card>
				</v-col>
				<v-col md="3">
					<v-card outlined rounded="lg">
						<v-card-text class="pb-0">
							<v-icon size="64">mdi-content-save-check-outline</v-icon>
						</v-card-text>
						<v-card-title>Autosave</v-card-title>
						<v-card-text>
							Soal otomatis tersimpan setelah siswa menjawab soal
						</v-card-text>
					</v-card>
				</v-col>
				<v-col md="3">
					<v-card outlined rounded="lg">
						<v-card-text class="pb-0">
							<v-icon size="64">mdi-domino-mask</v-icon>
						</v-card-text>
						<v-card-title>Analisis kecurangan</v-card-title>
						<v-card-text>
							Tersedia laporan indikasi kecurangan saat ujian
						</v-card-text>
					</v-card>
				</v-col>
				<v-col md="3">
					<v-card outlined rounded="lg">
						<v-card-text class="pb-0">
							<v-icon size="64">mdi-account-group-outline</v-icon>
						</v-card-text>
						<v-card-title>Batch</v-card-title>
						<v-card-text>
							Ujian dapat dibagi menjadi beberapa batch
						</v-card-text>
					</v-card>
				</v-col>
				<v-col md="3">
					<v-card outlined rounded="lg">
						<v-card-text class="pb-0">
							<v-icon size="64">mdi-microsoft-excel</v-icon>
						</v-card-text>
						<v-card-title>Export Hasil</v-card-title>
						<v-card-text>
							Hasil ujian dapat di export ke format excel
						</v-card-text>
					</v-card>
				</v-col>
				<v-col md="3">
					<v-card outlined rounded="lg">
						<v-card-text class="pb-0">
							<v-icon size="64">mdi-chart-bar-stacked</v-icon>
						</v-card-text>
						<v-card-title>Analisis Jawaban</v-card-title>
						<v-card-text>
							Tersedia laporan berapa lama rata-rata siswa menjawab soal
						</v-card-text>
					</v-card>
				</v-col>
			</v-row>
		</v-container>
	</div>
</div>
</template>
<script>
export default {
	layout:'blank',
	data: () => ({
		role: ['sekolah', 'guru', 'siswa', 'calon siswa'],
		roleDipilih: 'calon',
    }),
	methods:{
		handelMasuk:function(){
			if(this.$auth.user){
				this.$router.push("/apps/siswa")
			}else{
				this.$auth
					.loginWith('google')
					.catch((err) => {
						// eslint-disable-next-line no-console
						console.error(err)
						this.error = err.response?.data
					})
			}
			
		}
	}
}
</script>
