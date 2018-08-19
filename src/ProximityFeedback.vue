<script>
export default {
    props: {
        tag: {
            type: String,
            required: false,
            default: 'span'
        },
        animationClass: {
            type: String,
            required: true
        },
        distance: {
            type: Object,
            required: false,
            default() {
                return {
                    min: 0,
                    max: 100
                }
            }
        },
        divideBy: {
            type: Number,
            required: false,
            default: 100
        }
    },
    data() {
        return {
            proximity: null
        }
    },
    mounted() {
        this.start()
    },
    beforeDestroy() {
        this.stop()
    },
    computed: {
        checkProximity() {
            return this.proximity !== null && this.proximity <= this.distance.max ? true : false
        }
    },
    methods: {
        calculateDistance(e) {
            let elem = this.$el
            let mouseX = e.pageX
            let mouseY = e.pageY

            this.proximity = Math.floor(
                Math.sqrt(
                    Math.pow(
                        mouseX - (elem.getBoundingClientRect().left + elem.getBoundingClientRect().width / 2), 2
                    ) + Math.pow(
                        mouseY - (elem.getBoundingClientRect().top + elem.getBoundingClientRect().height / 2), 2
                    )
                )
            )
        },

        // tracker
        start() {
            document.addEventListener('mousemove', this.calculateDistance)
        },
        stop() {
            document.removeEventListener('mousemove', this.calculateDistance)
            this.proximity = null
        }
    },
    watch: {
        proximity(val) {
            if (this.checkProximity) {
                let min = this.distance.min

                Object.assign(this.$el.style, {
                    'animation-duration': (val <= min ? min : val) / this.divideBy + 's'
                })
            }
        },
        checkProximity(val) {
            this.$el.classList.toggle(this.animationClass, val)
        }
    },
    render(createElement) {
        return createElement(
            this.tag,
            this.$slots.default
        )
    }
}
</script>
