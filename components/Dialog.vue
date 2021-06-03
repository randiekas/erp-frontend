<template>
    <v-form ref="form">
        <!-- dialog -->
        <v-dialog
			v-model="isFetching"
			hide-overlay
			persistent
			width="300"
			>
			<v-card
				color="primary"
				dark
			>
				<v-card-text>
				Menyimpan ...
				<v-progress-linear
					indeterminate
					color="white"
					class="mb-0"
				></v-progress-linear>
				</v-card-text>
			</v-card>
		</v-dialog>
        <v-dialog
            v-if="dialog"
			v-model="modal"            
			width="300">
			<v-alert
                v-model="modal"
                border="top"
                color="green accent-4"
                dark
                dismissible
                type="success"
                >
                {{ dialog.message }}
            </v-alert>
		</v-dialog>
    </v-form>
</template>
<script>
export default {
    props: ['dialog', 'isFetching'],
    data: () => ({
        modal:false
    }),
    watch: {
        dialog: {
            // the callback will be called immediately after the start of the observation
            immediate: true, 
            handler (val, oldVal) {
                if(val && val.message){
                    this.modal  = true
                }
            // do your stuff
            }
        }
    }
}
</script>