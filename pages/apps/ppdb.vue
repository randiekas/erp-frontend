<template>
	<v-app>
        <div class="d-flex">
        <v-navigation-drawer
            color="muted"
            mini-variant
            permanent
            expand-on-hover
            style="height:100vh">
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
                ikon: "mdi-apps-box",
                nama: "Dashbord",
                link: "/apps/ppdb/beranda",
            },
            {
                ikon: "mdi-account-group",
                nama: "Jalur PPDB",
                link: "/apps/ppdb/jalur",
            },
            {
                ikon: "mdi-account-multiple-plus-outline",
                nama: "Seleksi Calon Siswa",
                link: "/apps/ppdb/calon",
            },
            {
                ikon: "mdi-account-multiple-check-outline",
                nama: "Penempatan",
                link: "/apps/ppdb/penerimaan",
            },
        ],
        
    }),
	methods:{
		
	}
}
</script>
