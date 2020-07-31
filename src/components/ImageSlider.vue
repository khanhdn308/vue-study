<template>
    <div class="upload-preview">
        <transition-group name="fade" tag="div">
            <div v-for="i in [currentIndex]" :key="i">
                <img :src="currentImg" alt="preview-upload"/>
            </div>
        </transition-group>
        <a class="prev" v-if="previewImages.length > 1" @click="prev" href="#">&#10094;</a>
        <a class="next" v-if="previewImages.length > 1" @click="next" href="#">&#10095;</a>
    </div>
</template>
<script>
export default {
    name: "ImageSlider",
    props: {
        previewImages: {
            type: Array
        }
    },
    data() {
        return {
            currentIndex: 0
        };
    },

    mounted: function () {
        // this.startSlide();
    },

    methods: {
        // startSlide: function() {
        //     this.timer = setInterval(this.next, 4000);
        // },

        next: function () {
            this.currentIndex += 1;
        },
        prev: function () {
            this.currentIndex -= 1;
        }
    },

    computed: {
        currentImg: function () {
            return this.previewImages[Math.abs(this.currentIndex) % this.previewImages.length];
        }
    }
};
</script>
<style>
img {
    width:180px;
}

.prev, .next {
    cursor: pointer;
    position: absolute;
    top: 60%;
    width: auto;
    padding: 8px;
    color: white;
    font-weight: bold;
    font-size: 18px;
    transition: 0.1s ease;
    border-radius: 0 4px 4px 0;
    text-decoration: none;
    user-select: none;
}

.next {
    right: 0;
}

.prev {
    left: 0;
}

.prev:hover, .next:hover {
    background-color: rgba(0,0,0,0.9);
}
</style>