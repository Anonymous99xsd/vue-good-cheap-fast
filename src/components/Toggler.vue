<template>
    <div class="toggler" :style="{...buttonSizeStyles}">
        <label>
            <input :checked="checked" @input="updateHandler" type="checkbox" />
            <span></span>
        </label>
        <strong>
            <slot></slot>
        </strong>
    </div>
</template>

<script>
export default {
    props: {
        size: {
            type: Number,
            default: 1,
        },
        checked: {
            type: Boolean,
            default: false,
        }
    },
    data () {
        return {
            buttonWidth: 50,
            buttonHeight: 30,
            toggleDiameter: 26,
            toggleWider: 34,
        }
    },
    computed: {
        buttonSizeStyles () {
            return {
                '--button-width': this.buttonWidth * this.size + 'px',
                '--button-height': this.buttonHeight * this.size + 'px',
                '--toggle-diameter': this.toggleDiameter * this.size + 'px',
                '--togger-wider': this.toggleWider * this.size + 'px',
            }
        }
    },
    methods: {
        updateHandler(e) {
            this.$emit('updated', e.target.checked)
        }
    },
}
</script>

<style scoped>
.toggler {
    --button-width: 500px;
    --button-height: 295px;
    --toggle-diameter: 255px;
    --button-toggle-offset: calc(
        (var(--button-height) - var(--toggle-diameter)) / 2
    );
    --toggle-shadow-offset: 10px;
    --togger-wider: 333px;
    --color-grey: #e9e9e9;
    --color-dark-grey: #39393d;
    --color-green: #30d158;
}

body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
}

span {
    display: inline-block;
    width: var(--button-width);
    height: var(--button-height);
    background-color: var(--color-grey);
    border-radius: calc(var(--button-height) / 2);
    position: relative;
    transition: background-color 0.3s ease-in-out;
}

span::after {
    content: '';
    display: inline-block;
    width: var(--toggle-diameter);
    height: var(--toggle-diameter);
    background-color: #fff;
    border-radius: calc(var(--toggle-diameter) / 2);
    position: absolute;
    top: var(--button-toggle-offset);
    left: 0;
    transform: translateX(var(--button-toggle-offset));
    box-shadow: var(--toggle-shadow-offset) 0
        calc(var(--toggle-shadow-offset) * 4) rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease-in-out, width 0.3s ease-in-out;
}

input[type='checkbox'] {
    display: none;
}

input[type='checkbox']:checked + span {
    background-color: var(--color-green);
}

input[type='checkbox']:checked + span::after {
    transform: translateX(
        calc(
            var(--button-width) - var(--toggle-diameter) -
                var(--button-toggle-offset)
        )
    );
    box-shadow: calc(-1 * var(--toggle-shadow-offset)) 0
        calc(var(--toggle-shadow-offset) * 4) rgba(0, 0, 0, 0.1);
}

input[type='checkbox']:active + span::after {
    width: var(--togger-wider);
}

input[type='checkbox']:checked:active + span::after {
    transform: translateX(
        calc(
            var(--button-width) - var(--togger-wider) -
                var(--button-toggle-offset)
        )
    );
}

.toggler {
    display: inline-flex;
    flex-direction: row;
}

.toggler strong {
    line-height: var(--button-height);
    font-size: var(--toggle-diameter);
    margin-left: calc(var(--toggle-diameter) / 4);
}

/* 深色模式 */
@media (prefers-color-scheme: dark) {
    body {
        background-color: #1c1c1e;
    }

    span {
        background-color: var(--color-dark-grey);
    }
}
</style>