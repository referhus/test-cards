<template>
    <div :class="classCheckbox">
        <div class="checkbox">
            <div
                @click="setActiveCheckbox(item)"
                class="checkbox-wrap"
                :class="{_active: item.checked}"
            >
                <div class="checkbox-icon">
                    <svg width="12" height="9" viewBox="0 0 12 9" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M1 4.5L5.28571 8L11 1" stroke="black"/>
                    </svg>
                </div>
                <span v-if="item.label">{{ item.label }}</span>
            </div>
        </div>
    </div>

</template>

<script>

    export default {
        props: {
            item: {
                type: Object,
                default: () => {}
            },
            activeCheckbox: {
                type: Number,
                default: -1
            },
            classCheckbox: {
                type: String,
                default: ''
            },
        },
        data() {
            return {
            }
        },
        methods: {
            setActiveCheckbox(i) {
                this.$emit('setCheckbox', i.id);
            },
        },
    }
</script>

<style>
    .checkbox-icon {
        position: relative;
        width: 16px;
        height: 16px;
        border: 1px solid var(--border);
        cursor: pointer;
    }

    .checkbox-wrap {
        display: flex;
        align-items: center;
        gap: 10px
    }

    .checkbox-icon svg {
        opacity: 0;
        transition: .3s;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }

    .checkbox-wrap._active .checkbox-icon {
        background: rgba(252, 230, 111, 1);
    }

    .checkbox-wrap._active .checkbox-icon svg {
        opacity: 1;
    }

</style>