<template>
<div>
    <p class="text-caption mb-0">{{ title }}</p>
    <p :class="`text-subtitle-2 mb-0 ${classSubtitle}`">{{ subtitle }}</p>
</div>
</template>
<script>
export default {
    props: ['title', 'subtitle', 'classSubtitle']
}
</script>