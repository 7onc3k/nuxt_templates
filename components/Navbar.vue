<template>
    <div class="relative">
        <div :class="{ 'h-screen': isOpen, 'h-20': !isOpen, 'lg:h-24': !isOpen }"
            class="transition-all duration-300 fixed top-0 left-0 w-full bg-blue-600 flex flex-col justify-between">

            <!-- Logo and arrow icons will be hidden when a link is selected -->
            <div :class="{ 'fade-out': selectedLink }"
                class="flex justify-between items-center px-4 lg:px-8 absolute top-0 left-0 w-full h-20 lg:h-24">
                <h2 class="text-white text-2xl lg:text-3xl ml-4 lg:ml-0">LOGO</h2>
                <div v-if="!isOpen" @click="toggleMenu" class="cursor-pointer mr-4 lg:mr-0">
                    <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 lg:w-8 lg:h-8 text-white" height="1em"
                        viewBox="0 0 448 512">
                        <path
                            d="M201.4 342.6c12.5 12.5 32.8 12.5 45.3 0l160-160c12.5-12.5 12.5-32.8 0-45.3s-32.8-12.5-45.3 0L224 274.7 86.6 137.4c-12.5-12.5-32.8-12.5-45.3 0s-12.5 32.8 0 45.3l160 160z" />
                    </svg>
                </div>
            </div>

            <div v-if="isOpen"
                class="flex flex-col justify-center items-center flex-grow space-y-8 lg:space-y-12 mt-24 lg:mt-28">
                <a href="#works" @click="navigate('works', $event)"
                    :class="{ 'selected': selectedLink === 'works', 'move': move && selectedLink === 'works', 'fade-out': fadeOut && selectedLink !== 'works' }"
                    class="text-white text-4xl lg:text-5xl">Works</a>
                <a href="#pricing" @click="navigate('pricing', $event)"
                    :class="{ 'selected': selectedLink === 'pricing', 'move': move && selectedLink === 'pricing', 'fade-out': fadeOut && selectedLink !== 'pricing' }"
                    class="text-white text-4xl lg:text-5xl">Pricing</a>
                <a href="#contact" @click="navigate('contact', $event)"
                    :class="{ 'selected': selectedLink === 'contact', 'move': move && selectedLink === 'contact', 'fade-out': fadeOut && selectedLink !== 'contact' }"
                    class="text-white text-4xl lg:text-5xl">Contact</a>
            </div>

            <div :class="{ 'fade-out': selectedLink }" v-if="isOpen" @click="toggleMenu" class="cursor-pointer flex justify-end items-center h-20 lg:h-24 px-4 lg:px-8 mr-4 lg:mr-0">
                <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 lg:w-8 lg:h-8 text-white" height="1em"
                    viewBox="0 0 448 512">
                    <path
                        d="M201.4 137.4c12.5-12.5 32.8-12.5 45.3 0l160 160c12.5 12.5 12.5 32.8 0 45.3s-32.8 12.5-45.3 0L224 205.3 86.6 342.6c-12.5 12.5-32.8 12.5-45.3 0s-12.5-32.8 0-45.3l160-160z" />
                </svg>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            isOpen: false,
            selectedLink: null,
            move: false,
            fadeOut: false,
            isMobile: window.innerWidth <= 768
        };
    },
    mounted() {
        window.addEventListener('resize', this.checkMobile);
        this.checkMobile(); // Ověříme zařízení při načtení stránky
    },
    beforeDestroy() {
        window.removeEventListener('resize', this.checkMobile);
    },
    methods: {
        checkMobile() {
            this.isMobile = window.innerWidth <= 768; 
        },
        toggleMenu() {
            this.isOpen = !this.isOpen;
        },
        // ... (ostatní metody zůstávají stejné)
        navigate(link, event) {
            this.selectedLink = link;

            // Všechny prvky, kromě vybraného odkazu, zprůhlední
            setTimeout(() => {
                this.fadeOut = true;
            }, 100);

            // Vybraný odkaz se posune na své místo
            setTimeout(() => {
                let targetPosition = this.isMobile ? 112 : 144; 
                let linkPosition = event.target.getBoundingClientRect().top;
                let moveDistance = linkPosition - targetPosition;

                event.target.style.transform = `translateY(-${moveDistance}px)`;
                this.move = true;
            }, 300);

            // Pozadí navbaru zprůhlední
            setTimeout(() => {
                document.querySelector('.bg-blue-600').style.opacity = '0';
            }, 600);

            // Vybraný odkaz zprůhlední
            setTimeout(() => {
                event.target.style.opacity = '0';
            }, 900);

            // Reset stavu po všech animacích
            setTimeout(() => {
                this.isOpen = false;
                this.fadeOut = false;
                this.move = false;
                this.selectedLink = null;
            }, 1200);
        }
    },
};
</script>

<style scoped>
.fade-out {
    opacity: 0;
    transition: opacity 0.3s ease-out;
}

.move {
    transition: transform 0.3s ease-out;
}
</style>