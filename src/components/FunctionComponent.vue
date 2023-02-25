<template>
    <div class="Score">
        Your Score: {{ player }} : {{ computer }} Computer Score
    </div>
    
</template>

<script>
export default{
    data(){
        return{
            player:0,
            computer:0
        }
    }
}
</script>

<style>
.Score
{
    display: flex;
    justify-content: center;
    font-size: 150%;
    margin-top: 1%;
}
</style>