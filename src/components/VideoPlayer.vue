<template>
    <v-card>
        <v-hover v-slot="{ isHovering, props }">

            <v-img v-if="!isPlaying" height="100" :src="poster" class="align-end" cover
                gradient="to bottom, rgba(0,0,0..1), rgba(0,0,0..5)" v-bind="props">

                <v-overlay :model-value="isHovering" contained class="align-center justify-center">
                    <v-btn icon @click="isPlaying = !isPlaying">
                        <v-icon>mdi-play-circle-outline</v-icon>
                    </v-btn>
                </v-overlay>
            </v-img>
            <v-card-title class="">
                {{ title }}
            </v-card-title>
        </v-hover>
    </v-card>
    <v-card-text>
        <v-row>
            <v-col cols="12">
                <v-progress-linear v-if="isPlaying" indeterminate color="primary"></v-progress-linear>
            </v-col>
        </v-row>
        <div v-if="isPlaying">
            <video controls autoplay>
                <source :src="url" type="video/mp4">


            </video>
        </div>
    </v-card-text>
</template>
<script>
export default {
    props: {
        title: String,
        url: String,
        poster: String
    },
    data: () => ({
        isPlaying: false
    }),
}

</script>