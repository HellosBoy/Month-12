<template>
    <div>
        <img @click="$emit('changeUrl', info.image)" :src="info.image" alt="">
    </div>
</template> 

<script>
export default {
    props: ['info']                                                              
}
</script>11111

<style scoped>
img {
    width: 100%;
}

</style>