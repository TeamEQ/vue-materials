<template>
    <ul class="collapsible"
        :data-collapsible="type"
        :class="classes"
    >
        <slot></slot>
    </ul>
</template>

<script type="text/babel">    
    import IsLoadable from '../mixins/is-loadable'

    export default {
        name: 'TeamEqCollapsible',
        
        mixins: [
            IsLoadable
        ],

        props: {
            collapse: {
                type: Boolean,
                default: false
            },

            expand: {
                type: Boolean,
                default: false
            },

            params: {
                type: Object,
                default() {
                    return {
                        accordion: false
                    }
                }
            },

            popout: {
                type: Boolean,
                default: false
            },

            openedAtStart: {
                type: [Boolean, Number],
                default: false
            }
        },

        watch: {
            openedAtStart(value) {
                if (value) {
                    $(this.$el).collapsible('open', value);                   
                }
            }
        },

        computed: {
            classes () {
                return {
                    'popout': this.popout
                }
            },

            type () {
                if (this.collapse) return 'accordion'
                if (this.expand)  return 'expandable'
            }
        },

        methods: {
            init () {
                $(this.$el).collapsible(this.params)
            }
        }
    }
</script>
