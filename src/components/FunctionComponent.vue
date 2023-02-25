<template>
    <div class="Score">
        Your Score: {{ player }} : {{ computer }} Computer Score
    </div>
    <div class="Questions">
        {{ questions[counter] }}
    </div>
    
</template>

<script>
import axios from 'axios'
export default{
    data(){
        return{
            player:0,
            computer:0,
            questions:[],
            options:[],
            rightAns:[],
            counter:0
        }
    },
    mounted(){
        axios.get('https://opentdb.com/api.php?amount=10&category=21&difficulty=easy&type=multiple')
        .then((data)=>{
            for(var i=0;i<10;i++){
                this.questions.push(data.data.results[i].question);
                var opt=[];
                opt.push(data.data.results[i].incorrect_answers[0]);
                opt.push(data.data.results[i].incorrect_answers[1]);
                opt.push(data.data.results[i].incorrect_answers[2]);
                opt.push(data.data.results[i].correct_answer);
                
                for (let i = opt.length - 1; i > 0; i--) {
                    const j = Math.floor(Math.random() * (i + 1));
                    [opt[i], opt[j]] = [opt[j], opt[i]];
                }

                this.options.push(opt);
                this.rightAns.push(data.data.results[i].correct_answer);
            }
        })
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