<template>
    <img class="img_song" :src="thumbnailM" alt="" :class="{animation: isAnimating}">
    <div class="infor">
        <p class="name_song">{{ name_song }}</p>
        <small class="artist_Name">{{ artist_Name }}</small>
    </div>
    <div class="playerbar__container">
        <span class="icon__container">
            <svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="shuffle" class="svg-inline--fa fa-shuffle " role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" type="rounded"><path fill="currentColor" d="M424.1 287c-15.13-15.12-40.1-4.426-40.1 16.97V352H336L153.6 108.8C147.6 100.8 138.1 96 128 96H32C14.31 96 0 110.3 0 128s14.31 32 32 32h80l182.4 243.2C300.4 411.3 309.9 416 320 416h63.97v47.94c0 21.39 25.86 32.12 40.99 17l79.1-79.98c9.387-9.387 9.387-24.59 0-33.97L424.1 287zM336 160h47.97v48.03c0 21.39 25.87 32.09 40.1 16.97l79.1-79.98c9.387-9.391 9.385-24.59-.0013-33.97l-79.1-79.98c-15.13-15.12-40.99-4.391-40.99 17V96H320c-10.06 0-19.56 4.75-25.59 12.81L254 162.7L293.1 216L336 160zM112 352H32c-17.69 0-32 14.31-32 32s14.31 32 32 32h96c10.06 0 19.56-4.75 25.59-12.81l40.4-53.87L154 296L112 352z"></path></svg>
            <svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="backward-step" class="svg-inline--fa fa-backward-step " role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 320 512" type="rounded"><path fill="currentColor" d="M31.1 64.03c-17.67 0-31.1 14.33-31.1 32v319.9c0 17.67 14.33 32 32 32C49.67 447.1 64 433.6 64 415.1V96.03C64 78.36 49.67 64.03 31.1 64.03zM267.5 71.41l-192 159.1C67.82 237.8 64 246.9 64 256c0 9.094 3.82 18.18 11.44 24.62l192 159.1c20.63 17.12 52.51 2.75 52.51-24.62v-319.9C319.1 68.66 288.1 54.28 267.5 71.41z"></path></svg>
            <svg v-if="checkAudio==true" @click="Play" aria-hidden="true" focusable="false" data-prefix="fas" data-icon="circle-play" class="svg-inline--fa fa-circle-play " role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" type="rounded"><path fill="currentColor" d="M512 256C512 397.4 397.4 512 256 512C114.6 512 0 397.4 0 256C0 114.6 114.6 0 256 0C397.4 0 512 114.6 512 256zM176 168V344C176 352.7 180.7 360.7 188.3 364.9C195.8 369.2 205.1 369 212.5 364.5L356.5 276.5C363.6 272.1 368 264.4 368 256C368 247.6 363.6 239.9 356.5 235.5L212.5 147.5C205.1 142.1 195.8 142.8 188.3 147.1C180.7 151.3 176 159.3 176 168V168z"></path></svg>
            <svg v-else @click="Pause" aria-hidden="true" focusable="false" data-prefix="fas" data-icon="circle-pause" class="svg-inline--fa fa-circle-pause " role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" type="rounded"><path fill="currentColor" d="M256 0C114.6 0 0 114.6 0 256s114.6 256 256 256s256-114.6 256-256S397.4 0 256 0zM224 191.1v128C224 337.7 209.7 352 192 352S160 337.7 160 320V191.1C160 174.3 174.3 160 191.1 160S224 174.3 224 191.1zM352 191.1v128C352 337.7 337.7 352 320 352S288 337.7 288 320V191.1C288 174.3 302.3 160 319.1 160S352 174.3 352 191.1z"></path></svg>
            <svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="forward-step" class="svg-inline--fa fa-forward-step " role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 320 512" type="rounded"><path fill="currentColor" d="M287.1 447.1c17.67 0 31.1-14.33 31.1-32V96.03c0-17.67-14.33-32-32-32c-17.67 0-31.1 14.33-31.1 31.1v319.9C255.1 433.6 270.3 447.1 287.1 447.1zM52.51 440.6l192-159.1c7.625-6.436 11.43-15.53 11.43-24.62c0-9.094-3.809-18.18-11.43-24.62l-192-159.1C31.88 54.28 0 68.66 0 96.03v319.9C0 443.3 31.88 457.7 52.51 440.6z"></path></svg>
            <svg @click="Repeat" aria-hidden="true" focusable="false" data-prefix="fas" data-icon="repeat" class="svg-inline--fa fa-repeat " role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" type="rounded"><path fill="currentColor" d="M480 256c-17.67 0-32 14.31-32 32c0 52.94-43.06 96-96 96H192L192 344c0-9.469-5.578-18.06-14.23-21.94C169.1 318.3 159 319.8 151.9 326.2l-80 72C66.89 402.7 64 409.2 64 416s2.891 13.28 7.938 17.84l80 72C156.4 509.9 162.2 512 168 512c3.312 0 6.615-.6875 9.756-2.062C186.4 506.1 192 497.5 192 488L192 448h160c88.22 0 160-71.78 160-160C512 270.3 497.7 256 480 256zM160 128h159.1L320 168c0 9.469 5.578 18.06 14.23 21.94C337.4 191.3 340.7 192 343.1 192c5.812 0 11.57-2.125 16.07-6.156l80-72C445.1 109.3 448 102.8 448 95.1s-2.891-13.28-7.938-17.84l-80-72c-7.047-6.312-17.19-7.875-25.83-4.094C325.6 5.938 319.1 14.53 319.1 24L320 64H160C71.78 64 0 135.8 0 224c0 17.69 14.33 32 32 32s32-14.31 32-32C64 171.1 107.1 128 160 128z"></path></svg>
            <audio ref="audio" :src="url_song" controls autoplay @play="addAnimation" @pause="removeAnimation" @timeupdate="updateProgress" @ended="resetProgress">
            </audio>
        </span>
        <div class="volumn">
            <svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="volume-high" class="svg-inline--fa fa-volume-high " role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 512"><path fill="currentColor" d="M412.6 182c-10.28-8.334-25.41-6.867-33.75 3.402c-8.406 10.24-6.906 25.35 3.375 33.74C393.5 228.4 400 241.8 400 255.1c0 14.17-6.5 27.59-17.81 36.83c-10.28 8.396-11.78 23.5-3.375 33.74c4.719 5.806 11.62 8.802 18.56 8.802c5.344 0 10.75-1.779 15.19-5.399C435.1 311.5 448 284.6 448 255.1S435.1 200.4 412.6 182zM473.1 108.2c-10.22-8.334-25.34-6.898-33.78 3.34c-8.406 10.24-6.906 25.35 3.344 33.74C476.6 172.1 496 213.3 496 255.1s-19.44 82.1-53.31 110.7c-10.25 8.396-11.75 23.5-3.344 33.74c4.75 5.775 11.62 8.771 18.56 8.771c5.375 0 10.75-1.779 15.22-5.431C518.2 366.9 544 313 544 255.1S518.2 145 473.1 108.2zM534.4 33.4c-10.22-8.334-25.34-6.867-33.78 3.34c-8.406 10.24-6.906 25.35 3.344 33.74C559.9 116.3 592 183.9 592 255.1s-32.09 139.7-88.06 185.5c-10.25 8.396-11.75 23.5-3.344 33.74C505.3 481 512.2 484 519.2 484c5.375 0 10.75-1.779 15.22-5.431C601.5 423.6 640 342.5 640 255.1S601.5 88.34 534.4 33.4zM301.2 34.98c-11.5-5.181-25.01-3.076-34.43 5.29L131.8 160.1H48c-26.51 0-48 21.48-48 47.96v95.92c0 26.48 21.49 47.96 48 47.96h83.84l134.9 119.8C272.7 477 280.3 479.8 288 479.8c4.438 0 8.959-.9314 13.16-2.835C312.7 471.8 320 460.4 320 447.9V64.12C320 51.55 312.7 40.13 301.2 34.98z"></path></svg>
            <input type="range" name="" id="" min="0" max="100">
        </div>
        <input type="range" min="0" max="100">
    </div>
    
</template>

<script>
export default {
    props: {
        url_song: String,
        thumbnailM: String,
        name_song: String,
        artist_Name: String,
    },
    data(){
        return{
            checkAudio: true,
            isAnimating: false
        }
    },
    methods: {
        Play() {
            this.$refs.audio.play();
        },
        Pause(){
            this.$refs.audio.pause();
        },
        Repeat(){
            this.$refs.audio.loop();
        },
        addAnimation() {
            this.checkAudio = false;
            this.isAnimating = true;
        },
        removeAnimation() {
            this.checkAudio = true;
            this.isAnimating = false;
        }
    },
    watch:  {
        url_song(){
            this.checkAudio = false;
        }
    },
}
</script>

<style scoped>
.name_song,.artist_Name{
    margin: 0;
}
.name_song{
    font-size: 17px;
    font-weight: 600;
    margin-bottom: 4px;
}
.artist_Name{
    font-size: 12px;
    font-weight: 300;
}
img{
    width: 70px;
    border-radius: 50%;
    position: fixed;
    bottom: 15px;
    left: 20px;
    z-index: 4;
}
.animation{
    animation-fill-mode: backwards;
    animation: spin 7s linear infinite;
}
.infor{
    position: fixed;
    bottom: 25px;
    left: 110px;
    z-index: 4;
    color: #ffff;
}
.volumn{
    position: fixed;
    bottom: 25px;
    right: 70px;
    z-index: 4;
    color: #ffff;
}
@keyframes spin {
    from {
        transform: rotate(0deg);
    }
    to {
        transform: rotate(360deg);
    }
}

audio{
    display: none;
}

input{
    width: 200px;
    margin-top: 12px;
    background: rgb(0,255,127);
}
.container{
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    height: 100px;
}
.playerbar__container{
    box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
    background-color: #233329;
    position: fixed;
    z-index: 3;
    bottom: 0;
    left: 0;
    right: 0;
    height: 100px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
.icon__container{
    display: flex;
    width: 250px;
    justify-content: space-between;
}
svg{
    width: 39px;
    color: rgb(192,192,192);
    cursor: pointer;
}
svg:hover{
    color: rgb(0,250,154);
}
.fa-shuffle,.fa-repeat{
    width: 20px;
}
.fa-backward-step,.fa-forward-step{
    width: 18px;
}
.fa-circle-play,.fa-circle-pause{
    color: rgb(0,250,154);
    transition-delay: .1s;
    transition: .2s;
}
.fa-circle-pause:hover{
    transform: scale(1.1);
}
.fa-circle-play:hover{
    transform: scale(1.1);
}
</style>