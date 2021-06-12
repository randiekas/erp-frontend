<template>
	<div>
		<Head 
			title="Hasil" 
			subtitle="Pengumuman Hasil Seleksi Penerimaan Siswa Baru"
			color="text--black"/>
		<v-alert
            border="left"
            close-text="Close Alert"
            color="deep-purple accent-4"
            dark>
            Setelah kamu diterima, segera lakukan daftar ulang dengan mengunjungi langsung sekolah tersebut.
		</v-alert>
		<v-row class="mt-6">
			<v-col v-for="(item, index) in data" :key="index" sm="12" md="4" cols="12">
				<v-card :class="`border--${warna[item.status]}`">
					<v-card-title class="pb-0">
						<v-icon left>mdi-school</v-icon>
						{{item.nama}}
					</v-card-title>
					<v-card-text>
						<div>{{item.alamat}}</div>
					</v-card-text>
					<v-card-actions>
						<v-spacer></v-spacer>
						<v-btn :color="warna[item.status]" text>
							{{ status[item.status] }}
							<v-icon right dark>{{ ikon[item.status] }}</v-icon>
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
	async asyncData({ $api }) {
		let data = (await $api.$get(`/api/v1/ppdb/pendaftaran/sekolah`)).data
		console.log(data)
		return {
			data
		}
	},
	data: () => ({
		status: [
			'Belum Diperiksa',
			'Diterima',
			'Tidak Diterima',
			'Daftar Ulang',
		],
		ikon: [
			'mdi-timer-sand',
			'mdi-account-check-outline',
			'mdi-account-remove-outline',
			'mdi-card-account-details-outline',
		],
		warna: [
			'primary',
			'success',
			'error',
			'primary',
		]
    }),
	methods:{
		
	}
}
</script>
