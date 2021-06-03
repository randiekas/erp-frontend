<template>
	<div>
		<Head 
			title="SD NEGRI KEUREA" 
			subtitle="Unnamed Road, Keurea, Kec. Bahodopi, Kabupaten Morowali, Sulawesi Tengah 94974"
			color="text--black"/>
			<v-row class="mt-6">
				<v-col sm="12" md="4" cols="12">
					<v-card>
						<v-img 
							height="auto"
							src="http://mtsummusshabri.com/public/asset_LogReg/images/bg-01.jpg"/>
					</v-card>
				</v-col>
				<v-col sm="12" md="8" cols="12">
					<v-card>
						<v-tabs
							v-model="tab"
							background-color="deep-purple accent-4"
							center-active
							dark>
							<v-tab key="profil">Profil</v-tab>
							<v-tab key="berita">Berita</v-tab>
							<v-tab key="galeri">Galeri</v-tab>
							<v-tab key="sdm">SDM</v-tab>
						</v-tabs>
					</v-card>
					<v-tabs-items v-model="tab">
						<v-tab-item key="profil">
							<v-card flat>
								<v-card-text>
									<p>Madrasah Tsanawiyah (MTs) Pesri Kendari terletak di jantung perkotaan Ibukota Provinsi, tepatnya di depan Kantor Wilayah Departemen Agama Prov. Sulawesi Tenggara, beralamat di Jln. Ahmad Yani No. 3 Kendari, Kelurahan Bende Kecamatan Kadia Kota Kendari. Secara formal, madrasah ini memiliki Nomor Pokok Sekolah Nasional (NPSN ): 40406047, dan Nomor Statistik Madrasah (NSM): 211274710003. Terdorong untuk meningkatkan citra lembaga, para pengelola madrasah mengundang tim assesor Badan Akreditasi Sekolah/Madrasah (BAS/M) Prov. Sulawesi Tenggara guna mendapatkan status akreditasi. Tahun 2013, BAN S/M menetapkan MTs Pesri Kendari mendapatkan status Akreditas “A” Saat ini, MTs Pesri Kendari memiliki sebanyak 42 guru dan staf (8 orang berstatus sebagai PNS dan 34 orang sebagai tenaga honorer). Jumlah siswa per Juli 2016, sebanyak 588 orang</p>
									<p class="text-h6">Visi</p>
									<p>
										“Menghasilkan lulusan yang berakhlakul karimah, peduli lingkungan hidup, mandiri, tangguh dalam berwirausaha, menguasai teknologi, dan siap bersaing dalam dunia usaha di tingkat nasional maupun internasional pada Tahun 2021.“
									</p>
									<p class="text-h6">Misi</p>
									<ul class=" text-gray-600 list-disc m-5">
										<li class="p-2">Meningkatkan keimanan dan ketaqwaan kepada Tuhan Yang Maha esa.</li>
										<li class="p-2">Meningkatkan kualitas manajemen dan sumber daya manusia.</li>
										<li class="p-2">Meningkatkan kepedulian peserta didik akan lingkungan hidup.</li>
										<li class="p-2">Meningkatkan pendidikan karakter disetiap mata pelajaran.</li>
										<li class="p-2">Meningkatkan kualitas pelayanan pendidikan dan pelatihan berbasis teknologi
											informasi dan komunikasi.</li>
										<li class="p-2">Meningkatkan kualitas dan kuantitas sarana dan prasarana pendidikan.</li>
										<li class="p-2">Meningkatkan keterserapan tamatan pada Dunia Usaha dan Industri bersekala
											nasional dan internasional.</li>
									</ul>
								</v-card-text>
							</v-card>
						</v-tab-item>
						<v-tab-item key="berita">

							<v-list two-line>
								<v-list-item-group
									v-model="selected"
									active-class="pink--text"
									multiple
								>
									<template v-for="(item, index) in items">
									<v-list-item :key="`berita${index}`">
										<template v-slot:default="{ active }">
										<v-list-item-content>
											<v-list-item-title v-text="item.title"></v-list-item-title>

											<v-list-item-subtitle
											class="text--primary"
											v-text="item.headline"
											></v-list-item-subtitle>

											<v-list-item-subtitle v-text="item.subtitle"></v-list-item-subtitle>
										</v-list-item-content>

										<v-list-item-action>
											<v-list-item-action-text v-text="item.action"></v-list-item-action-text>

											<v-icon
											v-if="!active"
											color="grey lighten-1"
											>
											mdi-star-outline
											</v-icon>

											<v-icon
											v-else
											color="yellow darken-3"
											>
											mdi-star
											</v-icon>
										</v-list-item-action>
										</template>
									</v-list-item>

									<v-divider
										v-if="index < items.length - 1"
										:key="index"
									></v-divider>
									</template>
								</v-list-item-group>
								</v-list>

						</v-tab-item>
						<v-tab-item key="galeri">
							<v-container>
							<v-row>
								<v-col
								v-for="n in 9"
								:key="n"
								class="d-flex child-flex"
								cols="4"
								>
								<v-img
									:src="`https://picsum.photos/500/300?image=${n * 5 + 10}`"
									:lazy-src="`https://picsum.photos/10/6?image=${n * 5 + 10}`"
									aspect-ratio="1"
									class="grey lighten-2"
								>
									<template v-slot:placeholder>
									<v-row
										class="fill-height ma-0"
										align="center"
										justify="center"
									>
										<v-progress-circular
										indeterminate
										color="grey lighten-5"
										></v-progress-circular>
									</v-row>
									</template>
								</v-img>
								</v-col>
							</v-row>
							</v-container>
						</v-tab-item>
						<v-tab-item key="sdm">
							<v-list subheader>
								<v-subheader>Staff</v-subheader>

								<v-list-item
									v-for="chat in recent"
									:key="chat.title"
								>
									<v-list-item-avatar>
									<v-img
										:alt="`${chat.title} avatar`"
										:src="chat.avatar"
									></v-img>
									</v-list-item-avatar>

									<v-list-item-content>
									<v-list-item-title v-text="chat.title"></v-list-item-title>
									<v-list-item-subtitle v-text="chat.role"></v-list-item-subtitle>
									</v-list-item-content>

									<v-list-item-icon>
									<v-icon :color="chat.active ? 'deep-purple accent-4' : 'grey'">
										mdi-message-outline
									</v-icon>
									</v-list-item-icon>
								</v-list-item>
								</v-list>

								<v-divider></v-divider>
						</v-tab-item>
					</v-tabs-items>
				</v-col>
				
			</v-row>
	</div>
</template>
<script>
export default {
	layout:'apps',
	data: () => ({
		tab:0,
		selected: [],
		items: [
			{
				action: '15 min',
				headline: 'Admin',
				subtitle: `Kendari (MTs Pesri) ---Kapolda Sultra Irjen Pol. Drs. Yan Sultra Indrajaya, SH, Wakapolda Sultra Brigjen Pol. Drs. Waris Agono, M.Si dan Dir Intelkam Kombes P`,
				title: 'Kapolda dan Wakapolda Sultra Sambangi Ummusshabri',
			},
			{
				action: '15 min',
				headline: 'Admin',
				subtitle: `Kendari (MTs Pesri) ---Kapolda Sultra Irjen Pol. Drs. Yan Sultra Indrajaya, SH, Wakapolda Sultra Brigjen Pol. Drs. Waris Agono, M.Si dan Dir Intelkam Kombes P`,
				title: 'Kapolda dan Wakapolda Sultra Sambangi Ummusshabri',
			},
		],
		recent: [
			{
				active: true,
				avatar: 'https://cdn.vuetifyjs.com/images/lists/1.jpg',
				title: 'Jason Oner',
				role: 'Kepala Sekolah',
			},
			{
				active: true,
				avatar: 'https://cdn.vuetifyjs.com/images/lists/2.jpg',
				title: 'Mike Carlson',
				role: 'Wakil Sekolah',
			},
			{
				avatar: 'https://cdn.vuetifyjs.com/images/lists/3.jpg',
				title: 'Cindy Baker',
				role: 'Keuangan',
			},
			{
				avatar: 'https://cdn.vuetifyjs.com/images/lists/4.jpg',
				title: 'Ali Connors',
				role: 'Administrasi',
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
