<template>
    <h1 class="container">Projections</h1>
    <div class="container first">
       
        <div class="container proj" v-for="item in projections" :key="item.id">
            <div class="left">
                <span>
                    data: {{ item.date_projection }}
                </span>
                <span> &nbsp;
                    prezzo: {{ item.ticket_price }}
                </span>
                <span>&nbsp;
                    fIlm: {{ item.movie.title }}
                </span>
                <span>&nbsp;
                    sala: {{ item.room.name }}
                </span>
                <span>&nbsp;
                    orario: {{ item.slot.time_slot }}
                </span>
            </div>
            <div class="right">
                <img class="img-fluid" :src=" item.movie.thumb" alt="">

            </div>
        </div>
    </div>
</template>

<script>
    import axios from "axios";
    import { store } from "../store";
    export default {
        name: "Projections",

        data() {
            return {
                store,
                projections: [],
            };
        },
        methods: {
            getProjections() {
                axios.get(this.store.apiBaseUrl + "/projections").then((response) => {
                    console.log(response.data);
                    this.projections = response.data.results;

                });
            },
        },
        mounted() {
            this.getProjections();
        },
    };
</script>


<style lang="scss" scoped>
.first{
    height: 500px;
    overflow-y: scroll;
    &::-webkit-scrollbar {
        display: none;
    }
}

.proj{
    width: 1000px;
    height: 300px;
    border: 1px solid black;
    border-radius: 20px;
    margin: 30px auto;
   display: flex;
   

    .left{
        width: 50%;
        height: 100%;
        border-right: 1px solid black;
        font-size: 2rem;
        display: flex;
        flex-direction: column;
        justify-content: center;
        
        
        
    }
    .right{
        width: 50%;
        height: 100%;
        overflow: hidden;

        img{
            width: 100%;
            height: 100%;
            object-fit: contain;
        }
    }
    
}


</style>