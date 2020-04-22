<template>
    <button class="InputButton" :class="`InputButton--${variant}`" @click.prevent="$emit('click')">
        <slot/>
    </button>
</template>

<script>
export default {
    props: {
        variant: {
            type: String
        }
    }
}
</script>

<style lang="scss">
.InputButton {
    width: 75px;
    height: 75px;
    font-size: 24px;
    border-radius: 100%;
    background-color:darkgrey;
    color: white;

    &--light {
        background-color:lightgrey;
        color: black;
    }

    &--orange {
        background-color:orange;
        color: white;
    }

}
</style>