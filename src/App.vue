<template>
  <div class="container-app">
    <div class="container-quiz">
      <div class="quiz-header">
        <h1>Quiz App</h1>
      </div>
      <div class="quiz-main" v-for="(element,index) in questions.slice(a,b)" v-bind:key="index" v-show="quiz">
        <div class="box-questions">
          <h2>Questions{{b}}/{{questions.length}}</h2>
          <p>{{element.question}}</p>
        </div>
        <div class="box-suggestions">
          <ul>
            <li v-for="(item,index) in element.suggestions" v-bind:key="index" :class="select ? check(item):''" v-on:click="selectResponse(item)">{{item.suggestion}}</li>
          </ul>
        </div>
        <div class="box-score" v-if="score_show">
          <h1>Your score is</h1>
          <p>{{score}}/{{questions.length}}</p>
          <button v-on:click="restartQuiz" type="button" name="button" class="restart-btn">Restart</button>
        </div>
      </div>
      <div class="quiz-footer">
        <div class="box-btn">
          <button type="button" name="button" @click="skipQuestion">Skip</button>
          <button type="button" name="button" @click="nextQuestion">Next</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  data(){
    return {
      questions:[
        {
          question:'How take glass',
          suggestions:[
            {suggestion:'byhand',correct:true},
            {suggestion:'withnose'},
            {suggestion:'withears'},
            {suggestion:'withlegs'}
          ]
        },
        {
          question:'How take helth',
          suggestions:[
            {suggestion:'byhand'},
            {suggestion:'withnose'},
            {suggestion:'withears',correct:true},
            {suggestion:'withlegs'}
          ]
        },
        {
          question:'How take cart',
          suggestions:[
            {suggestion:'byhand'},
            {suggestion:'withnose'},
            {suggestion:'withears'},
            {suggestion:'withlegs',correct:true}
          ]
        },
        {
          question:'How take pant',
          suggestions:[
            {suggestion:'byhand'},
            {suggestion:'withnose',correct:true},
            {suggestion:'withears'},
            {suggestion:'withlegs'}
          ]
        },
      ],
      a:0,
      b:1,
      select:false,
      score:0,
      quiz : true,
      score_show:false,
      next:false,
    };
  },
  methods:{
    selectResponse(e){
      this.select = true;
      this.next = true ;
      if(e.correct){
        this.score++;
      }
    },
    check(status){
      if(status.correct){
        return 'correct'
      }else{
        return 'incorrect'
      }
    },
    nextQuestion(){
      if (!this.next) {
        return;
      }

      if(this.questions.length - 1 == this.a){
        this.score_show = true;
        this.quiz = true;
      }else{
        this.a++;
        this.b++;
        this.select = false ;
      }

    },
    skipQuestion(){
      // if (!this.next) {
      //   return;
      // }
      if(this.questions.length - 1 == this.a){
        this.score_show = true;
        this.quiz = true;
      }else{
        this.a++;
        this.b++;
      }
    },
    restartQuiz(){
      Object.assign(this.$data, this.$options.data());
    }
  }
}
</script>
