<template>
    <div class="question-box-container">
        <br>
        <b-jumbotron >
               <template v-slot:header></template>

                <template v-slot:lead>
                   {{ currentQuestion.question}}
                </template> 
                <hr class="my-4">
                <b-list-group>
                    <b-list-group-item 
                        v-for="(answer , index) in answers"
                        :key="index"
                        @click="selectAnswer(index)"
                        :class="[selectedIndex === index ? 'selected' : '']"
                        >
                        {{answer}}   
                    </b-list-group-item>
                </b-list-group>
               <hr>
                <b-button @click="back" variant="primary" href="#">Back</b-button>&nbsp;&nbsp;
                <b-button variant="primary" href="#">submits</b-button>&nbsp;&nbsp;
                <b-button @click="next" variant="success" href="#">Next</b-button>
            
        </b-jumbotron>
    </div>
</template>


<script>
export default {
    props : {
        currentQuestion : Object,
        next : Function,
        back : Function
    },
    data(){
        return{
            selectedIndex : null
        }
    },
    computed:{
        answers(){
            let answers = [...this.currentQuestion.incorrect_answers]
            answers.push(this.currentQuestion.correct_answers)
            return answers
        }
    },
    methods:{
        selectAnswer(index){
            this.selectedIndex = index
            console.log(index)
        }
    },
    mounted(){
        console.log(this.currentQuestion)
    }
}
</script>

<style scoped>
    .list-group{
        margin-bottom: 15px;
    }

    .list-group-item:hover{
        background-color: #EEE;
    }
    .selected {
        background-color: lightblue;
    }

    .correct {
        background-color: green;
    }

    .incorrect {
        background-color: red;
    }

    .btn{
        margin : 0 5px;
    }

</style>