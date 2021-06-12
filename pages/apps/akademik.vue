<template>
	<v-app>
        <div class="d-flex">
        <v-navigation-drawer
            color="muted"
            mini-variant
            permanent
            expand-on-hover
            
            style="height:100vh;">
            <v-list
                dense
                nav
            >
                <v-list-item
                    v-for="(item, index) in menu"
                    :key="index"
                    :to="`${item.link}`"
                    link
                    color="primary"
                    >
                <v-list-item-icon>
                    <v-icon>{{ item.ikon }}</v-icon>
                </v-list-item-icon>

                <v-list-item-content>
                    <v-list-item-title>{{ item.nama }}</v-list-item-title>
                </v-list-item-content>
                </v-list-item>
            </v-list>
        </v-navigation-drawer>

        <v-main style="display: contents">
			<v-container class="grey lighten-5">
                <nuxt-child></nuxt-child>
            </v-container>
        </v-main>
        </div>
	</v-app>
</template>
<script>
export default {
	layout:'apps',
	data: () => ({
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
        
    }),
	methods:{
		
	}
}
</script>
