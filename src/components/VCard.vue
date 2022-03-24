<template>
    <div class="card">
        <a :href="anime.url" target="_blank">
            <img :src="anime.image_url" :alt="anime.title + ' Poster'">
            <h3>{{anime.title}}</h3>
        </a>
    </div>

    <!-- <div class="card">
        <a href="anime.url" target="_blank">
            <img src="../assets/image/download.png" alt="anime.title + ' Poster'">
            <h3>fasdfasdf</h3>
        </a>
    </div> -->
</template>

<script>
    export default {
        props:['anime'],
        
    }
</script>

<style lang="scss" scoped>


    a{
        text-decoration: none;
    }
    .card{

        flex: 1 1 30%;
        max-width: 30%;
        padding: 0px 8px;
        // background-color: gray;

        img{
            width: 100%;
            height: 300px;
            object-fit:cover;
            border-radius: 16px;
            box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.15);
            transition: 0.4s;
        }
        h3{
            padding: 16px;
            color:#313131;
            
        }
        &:hover{
            img{
                transform: scale(1.05);
                
            }
            h3{
               color:rgba(211, 214, 45, 0.884);
            }
        }
    }
</style>