<template>
	<div class="container">
		<div style="margin-top: 16px">
			<div class="align-center" style="margin-top:7rem;">
				<img src="https://prod-notion-assets.s3-us-west-2.amazonaws.com/front/product/hero.png" style="max-width:500px" class="w-100"/>
				<h2 class="mb-3 mt-3">Mohon tunggu . . .</h2>				
			</div>
			<p class="mt-2">
				Solusi monitoring belajar online yang manfaat nya dapat gunakan oleh : <b>Sekolah, Guru, Siswa dan orang tua</b>.
			</p>
		</div>
		<hr/>
	</div>
</template>
<script>
export default {
	layout:'blank',
	async asyncData({ $axios, $auth, redirect }) {
		let info			= false
		const queryString 	= window.location.href;
		const urlParams 	= new URLSearchParams(queryString)
		const token 		= `Bearer ${urlParams.get('access_token')}`
		const tipe			= $auth.$storage.getUniversal("loginType")
		await $axios.$post(`api/v1/akun/masuk_google`,{
			token:token,
			tipe:tipe,
			device:2,
			token_device:'',
		}).then((resp)=>{
			if(resp.status){	
				$auth.$storage.setUniversal("authToken", resp.data)
				$auth.$storage.setUniversal("_token.google", token)
				// redirect('/apps/beranda')
				window.location.href='/apps/beranda'
			}else{
				info	= resp.message
			}
		})
		return {
			info
		}
	}
	
}
</script>
<style>
body{
	font-size: 1.5em; /* currently ems cause chrome bug misinterpreting rems on body element */
}
</style>
