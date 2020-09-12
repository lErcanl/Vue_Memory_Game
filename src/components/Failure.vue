<template>
<div class="container">
    <h1>Maalesef bilemediniz</h1>
    <button @click="newGame">Yeni oyun</button>
</div>
</template>
<script>
export default {
        methods:{
            newGame(){
            this.$emit("activeComponentEvent","app-game-cards");

            }
        }
}
</script>

<style scoped>
    .container{
        position:absolute;
        top:0;
        left:0;
        width:100%;
        height:100%;
        display:flex;
        flex-direction: column;
        justify-content: center;
        align-items:center;
        background-color:darkred;
    }
    .container h1{
        font-size:333%;
        color:white;     
    }
    .container button{
        cursor:pointer;
        width:200px;
        color:darkred;
        height: 50px;
        font-size:15px;
        border-radius:50px;        
        outline: none;
        border:5px solid blue;
                transition:all .5s;

    }
    .container button:hover{
        background-color:lightgreen;
        color:#fff;

    }
</style>