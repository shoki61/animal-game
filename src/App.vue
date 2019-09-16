<template>
    <div >
        <div class="container" :class="colorDiv">
            <h1>TAHMİN ET!!!</h1>
            <div class="row">
                <div class="col-md-3 mt-3 mx-auto">
                    <h6 class="mt-1" style="color: salmon;">Doğrusu :</h6>
                       <h3 class="mt-3">{{ekle}}</h3>
                </div>
            </div>
            <transition name="fade" mode="out-in">
                <div key="button" v-if="ekle!==null">
                    <h5>Seçtiğin: <b>{{chosen}}</b></h5>
                    <div key="kz/kb" v-if="ekle!==null">
                        <app-kazandin v-if="ekle===chosen"></app-kazandin>
                        <app-kayibettin v-else></app-kayibettin>
                    </div>
                    <button  class="button-sil mb-2" @click="deleteText" >Yenile</button>
                </div>
                <div key="ul"  v-else>
                <ul  class="list-group  pb-1">
                    <li class="list list-group-item"
                        v-for="list in liste"
                        @click="appendList(list)"
                    >{{list}}</li>
                </ul>
                </div>
            </transition>
        </div>
    </div>
</template>

<script>
    import Kazandin from "./components/Kazandin";
import Kaybettin from "./components/Kaybettin";

export default {
    components:{
        appKazandin: Kazandin,
        appKayibettin: Kaybettin
    },
    data(){
        return{
            chosen:null,
            ekle:null,
            liste: ["Tavşan","Kuş","At","Köpek","Tavuk","Inek","Kaplumbağa","Kedi","Koyun","Deve","Fare","Balık","Ördek"]
        }
    },
    computed:{
            colorDiv:function(){
              return {
                  default: this.ekle==null,
                  red: this.ekle !== this.chosen,
                  green: this.ekle===this.chosen
              }
            }
    },
    methods: {
        deleteText(){
            this.ekle = null;
            this.chosen = null;
        },
        appendList(list){
            var index = Math.ceil(Math.random() * this.liste.length);
            this.ekle = this.liste[index-1] ;
            this.chosen = list;
        },
    },
};
</script>

<style>
    .container{
        background-color: purple;
        width: 100%;
        border-radius: 5px;
        height: 100vh;
        padding-top: 20px;
        text-align: center;
    }
    .col-md-3{
        width: 300px;
        height: 90px;
        background-color: whitesmoke;
        border-radius: 10px 10px 3px 3px;
        margin: 15px;
        color: purple;
        text-align: center !important;
    }
    .button-sil{
        background-color: whitesmoke;
        color: purple;
        padding: 3px 10px;
        border:none;
        cursor: pointer;
        border-radius: 10px;
        margin: auto;
        font-weight: 600;
    }
    .button-sil:hover{
        background-color: #e5e5e5;

    }
    .button-sil:focus{
        outline:0;
        box-shadow:0 0 0 .1rem #e2e2e2;
    }
    .list-group-item{
        width: 350px !important;
    }
    h3{
        margin: 15px;
    }
    h1{
        color: white;
    }
    h5{
        color: salmon;
    }
    b{
        color:white;
    }
    .red{
        background-color: darkred;
    }
    .green{
        background-color: green;
    }
    .default{
        background-color: purple;
    }
    .list{
        padding: 2px;
        width: 200px !important;
        text-align: center;
        cursor: pointer;
    }
    .list:hover{
        background-color: #ededed;
        color:purple;
        font-weight: 700;
    }
    ul{
        margin-left: 41%;
    }
    .fade-enter{
        opacity: 0;
    }
    .fade-enter-active{
        transition: opacity .3s;
    }
    .fade-leave{
    }
    .fade-leave-active{
        transition: opacity .3s;
        opacity: 0;
    }

</style>