<template>
    <div class="fs-20">
        <b>Your reaction time was: <span class="boldBold slateColor">{{ score }}</span> ms.</b>
    </div>
    <div class="fs-20">
        <b>You are <span class="slateColor">{{ text }}</span>.</b>
    </div>
</template>

<script>
export default {
    name: 'Result',
    props: [ 'score' ],
    data() {
        return {
            text: ''
        }
    },
    mounted() {
        if(this.score <= 1000) {
            this.text = 'fast snail';
        }
        else if(this.score <= 3000) {
            this.text = 'slow snail'
        }
        else this.text = 'old slow snail'
    }
}
</script>

<style scoped>
    .boldBold { font-weight: 900; }
    .slateColor { color: slateblue; text-decoration: underline; }
</style>