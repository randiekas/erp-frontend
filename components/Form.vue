<template>
    <v-form ref="form">
        <!-- form -->
        <div 
            v-for="(item, index) in fields.filter((item)=>item.form!=false)"
            :key="index">
            <!-- jika tipenya switct -->
            <v-switch 
                v-if="item.type==='switch'"
                :label="item.text"
                v-model="model[item.value]" 
                class="mt-0" />

            <!-- jika tipenya number -->
            <v-text-field
                v-else-if="item.type==='number'"
                type="number"
                :label="item.text"
                :hint="item.info?item.info[0]:''"
                v-model.number="model[item.value]"/>

            <!-- jika tipenya date -->
            <v-text-field
                v-else-if="item.type==='date'"
                type="date"
                :label="item.text"
                :hint="item.info?item.info[0]:''"
                v-model="model[item.value]"/>

            <!-- jika tipenya select -->
            <v-select
                v-else-if="item.type==='select'"
                v-model="model[item.value]"
                item-text="label"
                item-value="value"
                :items="item.options"
                :label="item.text"/>
            <!-- jika tipenya radio -->
            <v-radio-group 
                v-else-if="item.type==='radio'"
                v-model="model[item.value]">
                <template v-slot:label>
                    <div>{{ item.text }}</div>
                </template>
                <v-radio
                    v-for="(row, key) in item.options"
                    :key="key"
                    :label="row.label"
                    :value="row.value"/>
            </v-radio-group>

            <!-- jika tipenya textarea -->
            <v-textarea
                v-else-if="item.type==='textarea'"
                :label="item.text"
                :value="item.value"
                :hint="item.info?item.info[0]:''"
                v-model="model[item.value]"/>
                
            <!-- jika tipenya file -->
            <ButtonGDrive 
                v-else-if="item.type==='file'"
                :index="index"
                :label="item.text"
                :hint="item.info?item.info[0]:''"
                :onUploaded="(file)=>{model[item.value]=file}"
                v-model="model[item.value]"/>
                <!-- <v-file-input
                accept="image/pdf"
                :label="item.text"
                :hint="item.info?item.info[0]:''"
                v-model="model[item.value]"/> -->
            
            <v-text-field
                v-else-if="item.type==='openfile'"
                :label="item.text"
                :hint="item.info?item.info[0]:''"
                v-model="model[item.value]">
                <v-btn
                    small
                    slot="prepend"
                    :href="model[item.value]"
                    target="_blank">
                    <v-icon left dark>mdi-launch</v-icon>
                    Lihat File
                </v-btn>
            </v-text-field>
            
            <!-- jika tipenya text -->
            <v-text-field
                v-else
                :label="item.text"
                :hint="item.info?item.info[0]:''"
                v-model="model[item.value]"/>
        </div>
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
    props: ['fields', 'model', 'dialog', 'isFetching'],
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