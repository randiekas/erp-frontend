<template>
	<div class="d-flex" style="height:100vh;">
	<v-col class="mx-auto my-auto" xs="12" md="8" style="justify-content:center">
		<v-card elevation="4">
			<v-row no-gutters>
			<v-col xs="12" md="5" class="primary d-flex py-4" cols="12">
				<div class="mx-auto my-auto text-center">
					<v-icon color="white" size="64">mdi-school</v-icon>
					<p class="display-1 white--text">IDISI</p>
					<p class="subtitle-2 white--text">Sistem Informasi Sekolah</p>
				</div>
			</v-col>
			<v-col xs="12" md="7">
				<v-card-title>Masuk</v-card-title>
				<v-card-subtitle class="pb-0">Gunakan akun email untuk melanjutkan</v-card-subtitle>
				<v-card-text>
					<v-radio-group v-model="roleDipilih">
						<v-radio
							v-for="(item, index) in role"
							:key="index"
							:label="item"
							:value="item.replace('calon siswa', 'calon')"
						></v-radio>
					</v-radio-group>
					<div class="text-right">
							<v-btn 
								v-on:click="handleSubmit"
								color="primary">
								<v-icon left>mdi-google</v-icon>
								Masuk
							</v-btn>
						</div>
				</v-card-text>
			</v-col>
			</v-row>
		</v-card>
	</v-col>
	</div>
</template>
<script>
export default {
	layout:'blank',
	data: () => ({
		role: ['admin', 'sekolah', 'guru', 'siswa', 'calon siswa'],
		roleDipilih: 'siswa',
    }),
	methods:{
		handleSubmit:function(){
			if(this.roleDipilih!="calon"){
				alert("Maaf, hari ini akses tersebut belum tersedia. akan tersedia besok")
				return false
			}
			this.error = null
			this.$auth.$storage.setUniversal("loginType", this.roleDipilih)
			return this.$auth
				.loginWith('google')
				.catch((err) => {
					// eslint-disable-next-line no-console
					console.error(err)
					this.error = err.response?.data
				})
		}
	}
}
</script>
