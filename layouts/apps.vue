<template>
	<v-app>
		<v-dialog
			v-model="confirmation.status"
			persistent
			width="450">
			<v-card
				color="primary"
				dark>
				<v-card-title>{{ confirmation.title }}</v-card-title>
				<v-card-text>
					{{ confirmation.message }}
				</v-card-text>
				<v-card-actions>
					<v-spacer/>
					<v-btn
						text
						@click="confirmation.status=false">
						Cancel
					</v-btn>
					<v-btn
						outlined
						@click="confirmation.handelOk(); confirmation.status=false">
						Continue
					</v-btn>
				</v-card-actions>
			</v-card>
		</v-dialog>
		<v-navigation-drawer
			v-model="drawer"
			:mini-variant="miniVariant"
			permanent
			expand-on-hover
			app>
			<v-list>
				<v-list-item class="px-2">
					<v-list-item-avatar>
					<v-img :src="user.picture"></v-img>
					</v-list-item-avatar>
				</v-list-item>

				<v-list-item link>
					<v-list-item-content>
					<v-list-item-title class="title">
						{{ user.name }}
					</v-list-item-title>
					<v-list-item-subtitle>{{ user.email }}</v-list-item-subtitle>
					</v-list-item-content>
				</v-list-item>
			</v-list>

			<v-divider></v-divider>

			<v-list>
				<v-list-item
					v-for="(item, i) in apps"
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
			<nuxt-child
				:setConfirmation="(item)=>confirmation=item"
				:setFetching="setFetching"
				:handelKeluar="handelKeluar"/>
		</v-main>

	</v-app>
</template>

<script>
export default {
	data () {
		// let user = this.$auth.user
		let user	= {
			name: 'randi eka setiawan',
			email: 'randiekas@gmail.com',
			picture: 'https://lh3.googleusercontent.com/a-/AOh14Gi4xaqxMKNwVPnZoD16EBOJZXF-6VMZSUn3PF8FNg=s96-c'
		}
		let tipe = "admin"
		if(!user){
			this.$router.push(`/`) 
		}
		return {
			user,
			clipped: false,
			drawer: false,
			fixed: false,
			miniVariant: false,
			right: true,
			rightDrawer: false,
			title: 'IDISI',
			tipe,
			isFetching: false,
			apps: [
				{
					"ikon": "mdi-account-supervisor-circle",
					"nama":"Siswa",
					"deskripsi":"Siswa",
					"link":"/apps/siswa"
				},
				{
					"ikon": "mdi-school",
					"nama":"Guru",
					"deskripsi":"Sistem Pengelolaan Data Akademik Terpadu",
					"link":"/apps/guru"
				},
			],
			confirmation: {
                status: false,
                title: '',
                message: '',
                handelOk: ()=>{},
            },
		}
	},
	methods:{
		handelKeluar: async function(){
			await localStorage.removeItem('tipe')
			await localStorage.removeItem("auth.authToken")
			await this.$auth.logout()	
		},
		setFetching: function(status){
            this.isFetching = status
        },
		handelMasuk: function(){
			localStorage.setItem('tipe', 'admin')
			return this.$auth
				.loginWith('google')
				.catch((err) => {
					// eslint-disable-next-line no-console
					console.error(err)
					this.error = err.response?.data
				})
		},
	},
}
</script>
<style>
.border--primary{
	border: 1px solid #4268F6!important
}
.border--success{
	border: 1px solid #4caf50!important
}
.border--error{
	border: 1px solid #ff5252!important
}
</style>