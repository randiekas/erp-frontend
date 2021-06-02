<template>
    <v-app-bar
        color="deep-purple accent-4"
        dense
        dark
        >
        <v-btn 
            icon
            :to="to"
            exact>
            <v-icon>mdi-chevron-left</v-icon>
        </v-btn>
        <v-toolbar-title>{{title}}</v-toolbar-title>
    </v-app-bar>
</template>
<script>
export default {
    props: ['title', 'to']
}
</script>