<template>

    <div class="sketch-outline">
        <slot/>

        <canvas class="hint" ref="canvas" :style="cmpStyle"/>
    </div>

</template>

<script>
import rough from 'roughjs'

export default {
    props: {
        padding: {
            type: Number,
            default: 20
        },
        color: {
            type: String,
            default: '#c00'
        }
    },
    data () {
        return {
            slotWidth: 0,
            slotHeight: 0,
            rc: null,
            context: null,
            updateInterval: null,
            focused: false
        }
    },
    mounted () {
        this.rc = rough.canvas(this.$refs.canvas)
        this.context = this.$refs.canvas.getContext('2d')

        // update 10x/second
        this.updateInterval = setInterval(this.update, 1000 / 10)
    },
    beforeDestroy () {
        clearInterval(this.updateInterval)
    },
    methods: {
        redrawHint () {
            this.rc.rectangle(
                this.padding / 2,
                this.padding / 2,
                this.slotWidth - this.padding,
                this.slotHeight - this.padding,
                {
                    stroke: this.color
                }
            )
        },
        update () {
            this.context.clearRect(0, 0, this.$refs.canvas.width, this.$refs.canvas.height)

            const slotRect = this.$slots.default[0].elm.getBoundingClientRect()

            this.slotWidth = slotRect.width + this.padding
            this.$refs.canvas.width = slotRect.width + this.padding

            this.slotHeight = slotRect.height + this.padding
            this.$refs.canvas.height = slotRect.height + this.padding

            this.redrawHint()
        }
    },
    computed: {
        cmpStyle () {
            return {
                width: `${this.slotWidth + this.padding}px`,
                height: `${this.slotHeight + this.padding}px`,
                top: `-${this.padding}px`,
                left: `-${this.padding}px`
            }
        }
    }
}

</script>

<style lang="scss">

div.sketch-outline {
    position: relative;
    display: inline-block;

    canvas.hint {
        position: absolute;
        pointer-events: none;
        opacity: 0;
        transition: opacity 0.3s;
    }

    // active state
    &:hover,
    &:focus-within {
        canvas.hint {
            opacity: 1;
        }
    }
}

</style>
