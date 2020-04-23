<template>
    <button
        :class="classNames"
        @click.prevent="$emit('click')">
        <slot/>
    </button>
</template>

<script>
export default {
    props: {
        variant: {
            type: String
        },
        highlight: {
            type: Boolean,
            default: false
        },
        wide: {
            type: Boolean,
            default: false
        }
    },
    computed: {
        classNames() {
            let classNames = 'InputButton';
            if (this.variant) classNames += ` InputButton--${this.variant}`;
            if (this.wide) classNames += ` InputButton--wide`;
            if (this.highlight) classNames += ' highlight';
            return classNames;
        }
    }
}
</script>

<style lang="scss">
$width: 75px;

.InputButton {
    width: $width;
    height: $width;
    font-size: 24px;
    border-radius: 100%;
    background-color:darkgrey;
    color: white;

    &--wide {
        width: $width * 2;
        border-radius: 15%;
    }

    &--light {
        background-color:lightgrey;
        color: black;
    }

    &--orange {
        background-color:orange;
        color: white;

        &.highlight {
            color:orange;
            background-color: white;
        }
    }

}
</style>