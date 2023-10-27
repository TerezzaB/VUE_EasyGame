<template>
    <div class="backdrop" v-if="showBlock" @click="stopTimer()">
        <div class="modal" :class="{ reaction_block: blockType === 'reaction_block' }" @click="stopTimer(), closeModal()">
           <slot></slot>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Block',
    props: [ 'blockType', 'delay' ],
    data() {
        return {
            showBlock: false,
            timer: null,
            reactionTime: 0
        }
    },

    methods: {
        closeModal() {
            this.$emit('closeEvent');
        },

        startTimer() {
            this.timer = setInterval(() => {
                this.reactionTime += 10;
            }, 10);
        },

        stopTimer() {
            clearInterval(this.timer);
            console.log('Reaction Time: ', this.reactionTime);
            this.$emit('end', this.reactionTime);
        }
    },

    mounted() {
        console.log('component mounted');
        setTimeout(() => {
            this.showBlock = true;
            this.startTimer();
            console.log(this.delay);
        }, this.delay)
    },

    updated() {
        console.log('component updated');
    },

    unmounted() {
        console.log('component unmounted');
    }
}

</script>

<style scoped>
    .backdrop { top: 0; position: fixed; background: rgba(0,0,0,0.5); width: 100%; height: 100%; }
    .modal { width: 400px; padding: 100px; margin: 100px auto; background: #FFF; border-radius: 10px; }
    .reaction_block { background: slateblue; color: #FFF; text-align: center; cursor: pointer; }
</style>