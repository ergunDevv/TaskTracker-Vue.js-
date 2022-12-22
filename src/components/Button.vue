<template>
    <button v-on:click="onClicked()" :style="{background:color}" class="btn"> {{ text }}</button>
</template>


<script>
export default {
    name: 'ButtonComponent',
    props:{
        text:String,
        color:String
    },
    methods:{
        onClicked(){
            console.log('HEY IM CLICKED')
        }
    }
}

</script>
