<template>
    <div class="Container" v-if="playOn">
        <div class="Score">
            Your Score: {{ player }} : {{ computer }} Computer Score
        </div>
        <div class="Questions">
            {{ questions[counter] }}
        </div>
        <div class="OptionsArea" v-if="called">
            <button @click="check('op1')" id="op1">{{ options[counter][0] }}</button> <br>
            <button @click="check('op2')" id="op2">{{ options[counter][1] }}</button> <br>
            <button @click="check('op3')" id="op3">{{ options[counter][2] }}</button> <br>
            <button @click="check('op4')" id="op4">{{ options[counter][3] }}</button> <br>
        </div>
        <div class="NextQuestion" v-if="called">
            <button @click="nextQues()" disabled="true" id="nextQ">Next Question</button>
        </div>
    </div>
    <div class="FinalScore" v-if="playOff">
        Your Final Score is {{ this.player }} against the Computers {{ this.computer }} <br>
        <a href=""><button>Start Over</button></a>
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
            counter:0,
            called:false,
            playOn:true,
            playOff:false
        }
    },
    mounted(){
        axios.get('https://opentdb.com/api.php?amount=10&category=21&difficulty=easy&type=multiple')
        .then((data)=>{
            for(var i=0;i<10;i++){
                var s=data.data.results[i].question;
                var replacedStr = s.replace(/&#039;/g, "'");
                replacedStr = replacedStr.replace(/&quot;/g, "''");
                this.questions.push(replacedStr);
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

                this.called=true;

            }
        })
    },
    methods:{
        check(id){
            var user_ans=""+document.getElementById(id).innerHTML;
            if(user_ans==this.rightAns[this.counter])
            {
                this.player++;
                document.getElementById(id).style.backgroundColor="rgb(64, 255, 47)";
            }
            else
            {
                this.computer++;
                document.getElementById(id).style.backgroundColor="rgb(255, 47, 47)";
            }
            document.getElementById('op1').disabled = true;
            document.getElementById('op2').disabled = true;
            document.getElementById('op3').disabled = true;
            document.getElementById('op4').disabled = true;
            document.getElementById('nextQ').disabled = false;
            document.getElementById('nextQ').style.backgroundColor="rgb(47, 161, 255)";
        },
        nextQues(){
            if(this.counter!=10){
                this.counter++;
                document.getElementById('nextQ').disabled = true;
                document.getElementById('op1').disabled = false;
                document.getElementById('op2').disabled = false;
                document.getElementById('op3').disabled = false;
                document.getElementById('op4').disabled = false;

                document.getElementById('op1').style.backgroundColor="rgb(47, 161, 255)";
                document.getElementById('op2').style.backgroundColor="rgb(47, 161, 255)";
                document.getElementById('op3').style.backgroundColor="rgb(47, 161, 255)";
                document.getElementById('op4').style.backgroundColor="rgb(47, 161, 255)";
                document.getElementById('nextQ').style.backgroundColor="rgb(95, 99, 102)";
            }
            if(this.counter==10)
            {
                this.playOn=false;
                this.playOff=true;
            }
        }
    }
}
</script>

<style>
.Score
{
    display: flex;
    justify-content: center;
    font-size: 200%;
    margin-top: 1%;
    margin-bottom: 3%;
}
button
{
    background-color:rgb(47, 161, 255) ;
    border: none;
    color: white;
    font-size: 150%;
    padding: 1%;
    margin: 0.5%;
}
.Questions
{
    font-size: 150%;
}
#nextQ
{
    background-color:rgb(95, 99, 102) ;
}
.Container
{
    margin-left: 10%;
    margin-right: 10%;
}
.FinalScore
{
    margin-left: 10%;
    margin-right: 10%;
    font-size: 150%;
    text-align: center;
    margin-top: 3%;
}
</style>