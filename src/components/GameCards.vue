<template>
<div class="game-area">
    <h1 class="title">Poğaça Nerede</h1>
    <h4 class="description">Açık olan kartlardan bir tanesine tıklayınız!</h4>
    <div class="container">
        <transition-group class="container" appear name="rotate-all">
        <app-card 
        @click.native="selectedElement=card.id"        
        :class="{'shadow':selectedElement==card.id}"
        v-for="card in cards" :card="card" :key="card.id"></app-card>
</transition-group>
</div>
<div class="container">
<transition mode="out-in" name="rotate">
<component @click.native="showCard(answer)" 
 :is="activeCard" 
:card="answer">
</component>
       </transition> 
       </div>
</div>
</template>
<script>
import card from "./Card";
import DefaultCard from "./DefaultCard";
export default {
        components:{
            appCard:card,
            appDefaultCard:DefaultCard
        },
        data(){

            return{
                activeCard:"app-default-card",
                answer:{},
                selectedElement:null,
                cards:[
                    {
                    id:1,
                    component:"app-card",
                    image:"/src/assets/card-1.jpg"
                },
                 {
                    id:2,
                    component:"app-card",
                    image:"/src/assets/card-2.jpg"
                },
                 {
                    id:3,
                    component:"app-card",
                    image:"/src/assets/card-3.jpg"
                },
                 {
                    id:4,
                    component:"app-card",
                    image:"/src/assets/card-4.jpg"
                },
                 {
                    id:5,
                    component:"app-card",
                    image:"/src/assets/card-5.jpg"
                }
                ]
            }
        },
        created(){
            let answer= Math.ceil(Math.random() * this.cards.length);
            this.answer=this.cards[answer -1];
            console.log(answer);
        },
        methods:{
            showCard(answer){
                if(this.selectedElement==null){

                    alert("lütfen bir eleman seçin");
                }
                else{
                    
                    this.activeCard=answer.component;
                    setTimeout(() => {
                         if(answer.id==this.selectedElement){
                    this.$emit("activeComponentEvent","app-celebrate");
                }
                else{
                    this.$emit("activeComponentEvent","app-failure");
                }
                        
                    }, 2000);
               

            }
            }
        }
}
</script>

<style scoped>
.title{
    text-align: center;
    color:blueviolet;
}
.description{
    color:grey;
    text-align: center;
}

.container{
    display: flex;
    justify-content: center;
    align-items: center;
}
.shadow{
    box-shadow:0px 15px 15px #30969f !important;
    transition:.5s;
}
.rotate-all-enter{

}
.rotate-all-enter-active{
        animation:rotate-all ease-in-out 3s;
}

.rotate-leave{

}
.rotate-leave-active{
    animation:rotate-out 1s ease-in-out forwards;

}
.rotate-enter{

}

.rotate-enter-active{
    animation:rotate-in 1s ease-in-out forwards;
}
@keyframes rotate-all{
    from{
        transform:rotateY(0);
    }
    to{
        transform:rotateY(1080deg);
    }
    
}

@keyframes rotate-in{
    from{
        transform:rotateY(90deg);
    }
    to{
    transform:rotateY(0);
    }

}
@keyframes rotate-out{
     from{
        transform:rotateY(0);
    }   
    to{
    transform:rotateY(90deg);
    }
}
</style>