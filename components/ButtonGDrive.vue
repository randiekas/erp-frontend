<template>
	<div>
		<!-- <v-file-input
			accept="image/pdf"
			:label="label"
			:hint="hint"
			v-on:change="handleUploadFile"/> -->
		<v-text-field
				:loading="uploading"
                :label="label"
                :hint="hint"
				v-bind:value="value" v-on:input="$emit('input', $event.target.value)">
			<v-btn
				:loading="uploading"
				small
				slot="prepend"
				v-on:click="handleGetToken">
				Pilih File
			</v-btn>
		</v-text-field>
		<!-- <button type="button" v-on:click="handleGetToken">{{uploading?`Sedang diunggah ${percentCompleted}% ...`:"Unggah File"}}</button> -->
		<input type="file" :id="`button-pilih-file-${index}`" class="d-none" v-on:change="handleUploadFile"/>
	</div>
</template>
<style>
</style>
<script>
  export default {
	data(){
		return {
			model: '',
			percentCompleted:0,
			uploading:false,
			info:false,
		}
	},
    props: ['index', 'label', 'name', 'type', 'note', 'value', 'placeholder', 'onUploaded', 'hint'],
	methods: {
		async handleGetToken(){
			this.setUploading(true)
			const access_token	= (await this.$api.$get(`/api/v1/google/accesstoken`)).data
			this.setUploading(false)
			if(access_token!=null){
				this.access_token	= access_token
				this.setUploading(false)
				document.getElementById(`button-pilih-file-${this.index}`).click()
			}else{
				alert('Unggah file tidak tersedia, silahkan hubungi wa admin 082126833236.')
				return false
			}
		},
		setUploading (value){
			this.uploading=value
		},

		// di method ini ada 2 step, upload ke google drive, lalu berikan akses publik di google drive
		async handleUploadFile(e){
			console.log(e)
			// await this.handleGetToken()
			// let metadata={
			// 	"title": "tes.png",
			// 	"mimeType": "jpg/png",
			// }

			let file 		= e.target.files[0]
			var formData 	= new FormData();
			this.setUploading(true)

			formData.append('file', file);

			let config = {
				method: 'post',
				url: 'https://www.googleapis.com/upload/drive/v3/files',
				headers: { 
					'Authorization': `Bearer ${this.access_token}`, 
					'Content-Type': 'application/json'
				},
				onUploadProgress: (progressEvent)=>{
					this.percentCompleted = Math.round((progressEvent.loaded * 100) / progressEvent.total)
				}
			};

			// handle upload file
			let config_upload_file 		= config
			config_upload_file.data		= formData
			const axios 				= this.$api
			axios(config_upload_file)
			.then((response)=>{
				let id_file						= response.data.id
				let config_upload_permission 	= config

				// handle permission
				config_upload_permission.url	= `https://www.googleapis.com/drive/v3/files/${id_file}/permissions`
				config_upload_permission.data	= {
					role:'reader',
					type:'anyone'
				}
				axios(config_upload_permission)
				.then((response)=>{
					this.setUploading(false)
					this.model = `https://drive.google.com/file/d/${id_file}/view?usp=sharing`
					this.onUploaded(`https://drive.google.com/file/d/${id_file}/view?usp=sharing`)
					// this.formData.lampiran	= `https://drive.google.com/file/d/${id_file}/view?usp=sharing`
					console.log(response.data)
				}).catch(function (error) {
					this.setUploading(false)
					console.log(error);
				});
			}).catch(function (error) {
				this.setUploading(false)
				console.log(error);
			});
		}
	}
  }
</script>
