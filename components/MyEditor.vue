<template>
    <client-only placeholder="loading...">
        <ckeditor-nuxt v-model="contentHolder" :config="editorConfig"  />
    </client-only>
</template>

<script>
export default {
    props: [ 'value' ],
    components: {
        'ckeditor-nuxt': () => { if (process.client) { return import('@blowstack/ckeditor-nuxt') } },
    },
    data() {
        return {
            editorConfig: {
                simpleUpload: {
                    uploadUrl: 'path_to_image_controller',
                    headers: {
                        'Authorization': 'optional_token'
                    }
                },
                removePlugins: ['Title'],
            },
            contentHolder: this.value
        }
    },
    watch: {
        contentHolder(value) {
            // HTML
            // const isSame = CKEDITOR.getHTML() === value

            // JSON
            // const isSame = JSON.stringify(this.editor.getJSON()) === JSON.stringify(value)

            // if (isSame) {
            //     return
            // }

            this.$emit('input', value)
            // CKEDITOR.commands.setContent(value, false)
        },
    }
}
</script>
<style>
    .ck-editor__editable {
        min-height: 250px;
    }
</style>
