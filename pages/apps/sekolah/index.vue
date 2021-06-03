<template>
	<div>
		<Head 
			title="Sekolah" 
			subtitle="Berikut daftar sekolah yang menerima ppdb (penerimaan siswa baru)"
			color="text--black"/>
		<v-row class="mt-6">
			<v-col v-for="(item, index) in sekolah" :key="index" sm="12" md="4" cols="12">
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
							Lihat Detil
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
		sekolah: [
				{
					"ikon": "mdi-school",
					"nama":"SD NEGRI KEUREA",
					"deskripsi":"Unnamed Road, Keurea, Kec. Bahodopi, Kabupaten Morowali, Sulawesi Tengah 94974",
					"link":"/apps/sekolah/detil"
				},
				{
					"ikon": "mdi-school",
					"nama":"SD NEGRI 1 Kujangsari",
					"deskripsi":"Unnamed Road, Keurea, Kec. Bahodopi, Kabupaten Morowali, Sulawesi Tengah 94974",
					"link":"/apps/sekolah/detil"
				},
				{
					"ikon": "mdi-school",
					"nama":"SD NEGRI 2 Kujangsari",
					"deskripsi":"Unnamed Road, Keurea, Kec. Bahodopi, Kabupaten Morowali, Sulawesi Tengah 94974",
					"link":"/apps/sekolah/detil"
				},
			],
		
    }),
	methods:{
		handleKonfirmasiHapus(){
			// console.log(this)
			this.dialogDelete	= true
		},
		handleHapus(){
			this.dialogDelete	= false
		}
	}
}
</script>
