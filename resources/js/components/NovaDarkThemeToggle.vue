<template>
    <button
            @click="toggle()"
            class="block no-underline text-90 hover:bg-30 p-3 w-full text-left dark-mode-toggle">
        <icon-toggle
                v-if="darkThemeOn"
                class="w-4 h-4 text-black align-baseline ml-1 mr-4 dark-mode-active"
                style=""></icon-toggle>
        <icon-toggle
                v-else
                class="w-4 h-4 text-black align-baseline ml-1 mr-4 dark-mode-disabled"></icon-toggle>
    </button>
</template>

<script>
    import IconToggle from './icons/IconToggle.vue';
    export default {
        name: "NovaDarkThemeToggle",
        props: {
            label: {
                type: String,
                required: false,
                default: function () {
                    return 'Dark Theme'
                }
            }
        },
        data: () => ({
            darkThemeOn: false
        }),
        components: {
            IconToggle
        },
        mounted() {

            let prefersDarkScheme = window.matchMedia(
                "(prefers-color-scheme: dark)"
            ).matches;

            if(prefersDarkScheme && localStorage.darkThemeOn === undefined) {
                localStorage.darkThemeOn = "true";
                this.darkThemeOn = "true";
            } else {
                this.darkThemeOn = localStorage.darkThemeOn === "true";
            }

            if (localStorage.darkThemeOn === "true") {
                document.querySelector('html').classList.add('nova-dark-theme');
                document.querySelector('body').classList.add('nova-dark-theme');
            }

            if (localStorage.darkThemeOn === "false") {
                document.querySelector('html').classList.remove('nova-dark-theme');
                document.querySelector('body').classList.remove('nova-dark-theme');
            }
        },
        methods: {
            toggle() {
                this.darkThemeOn = !this.darkThemeOn;
                localStorage.darkThemeOn = this.darkThemeOn.toString();
                document.querySelector('html').classList.toggle('nova-dark-theme');
                document.querySelector('body').classList.toggle('nova-dark-theme');
            }
        }
    }
</script>

<style scoped>
.dark-mode-toggle {
    position: fixed;
    bottom: 0px;
    right: 0px;
    width: 50px;
    height: 50px;
    background: #ff5500;
    border-radius: .6rem 0 0;
    padding: 1rem .6rem .6rem .8rem;
}
.nova-dark-theme .dark-mode-toggle {
    background: #161c22;
}
.dark-mode-toggle:hover {
    background-color: #ff5577;
}
.dark-mode-toggle:focus {
    outline: none;
}
.nova-dark-theme .dark-mode-toggle:hover{
    background: #ff5577;
}
.dark-mode-active {
    margin-bottom: -2px;
    color: #ff5500;
}
.dark-mode-disabled {
    margin-bottom: -2px;
    transform: rotate(180deg);
    color: rgb(255 255 255);
}
</style>
