<template>
    <div class="ui-skeleton" v-if="!show">
        <slot name="before"/>
    </div>

    <slot v-else/>
</template>

<script lang="ts" setup>

const props = defineProps<{
    show?: boolean;
}>();

</script>

<style lang="scss" scoped>

.ui-skeleton {
    display: flex;
    min-width: 16px;
    min-height: 16px;
    border-radius: 25px;
    align-items: center;
    justify-content: center;
    background: linear-gradient(100deg, transparent 40%, var(--color-primary) 50%, transparent 60%) var(--T);
    background-size: 200% 100%;
    background-position-x: 180%;
    animation: 1.5s Loading ease-in-out infinite;

    @keyframes Loading {
        to {
            background-position-x: -20%;
        }
    }
}

</style>