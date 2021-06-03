<template>
	<v-app>
		<v-navigation-drawer
			v-model="drawer"
			:mini-variant="miniVariant"
			permanent
			expand-on-hover
			app>

			<v-list>
				<v-list-item class="px-2">
					<v-list-item-avatar>
					<v-img src="https://randomuser.me/api/portraits/women/85.jpg"></v-img>
					</v-list-item-avatar>
				</v-list-item>

				<v-list-item link>
					<v-list-item-content>
					<v-list-item-title class="title">
						IDISI
					</v-list-item-title>
					<v-list-item-subtitle>Admin</v-list-item-subtitle>
					</v-list-item-content>
				</v-list-item>
			</v-list>

			<v-divider></v-divider>

			<v-list>
				<v-list-item
					color="primary"
					to="/apps/beranda">
					<v-list-item-action>
						<v-icon>mdi-apps</v-icon>
					</v-list-item-action>
					<v-list-item-content>
						<v-list-item-title v-text="'Beranda'" />
					</v-list-item-content>
				</v-list-item>
				<v-list-item
					v-for="(item, i) in apps[tipe]"
					:key="i"
					:to="item.link"
					color="primary">
					<v-list-item-action>
						<v-icon>{{ item.ikon }}</v-icon>
					</v-list-item-action>
					<v-list-item-content>
						<v-list-item-title v-text="item.nama" />
					</v-list-item-content>
				</v-list-item>
				<v-list-item
					color="primary"
					to="/">
					<v-list-item-action>
						<v-icon>mdi-logout</v-icon>
					</v-list-item-action>
					<v-list-item-content>
						<v-list-item-title v-text="'Keluar'" />
					</v-list-item-content>
				</v-list-item>
			</v-list>
		</v-navigation-drawer>

		<v-main>
			<v-container>
				<nuxt-child/>
			</v-container>
		</v-main>

		<v-navigation-drawer
		v-model="rightDrawer"
		:right="right"
		temporary
		fixed
		>
		<v-list>
			<v-list-item @click.native="right = !right">
			<v-list-item-action>
				<v-icon light>
				mdi-repeat
				</v-icon>
			</v-list-item-action>
			<v-list-item-title>Switch drawer (click me)</v-list-item-title>
			</v-list-item>
		</v-list>
		</v-navigation-drawer>
		
	</v-app>
</template>

<script>
export default {
	data () {
		return {
			clipped: false,
			drawer: false,
			fixed: false,
			
			miniVariant: false,
			right: true,
			rightDrawer: false,
			title: 'IDISI',
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
					"deskripsi":"Portal Informasi Sekolah yang menerima PPDB (pendaftaran peserta didik baru)",
					"link":"/apps/sekolah"
				},
			]
		}
		}
	}
}
</script>
<style>
.border--primary{
	border: 1px solid #4268F6!important
}
</style>