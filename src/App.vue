<script setup>


</script>

<template>
  <header>
    <h1>Rock Paper Scissors Love</h1>

  </header>
  <div id="app">
    <div class="pgbg">
        <div class="roundcon">
            <div class="roundind">
                <h2>{{ roundMessage }}</h2>
            </div>
        </div>
        <div class="scoreboard">
            <p>{{ scoreboardMessage }}</p>
        </div>
        <div class="game-container">
        <div class="team">
            
            <div class="team-info"  >
                <div class="imgframe">
                    <img  v-if="leftTeamChoice ===''" src="/src/assets/img/ScissorF.png" alt="Scissors">
                    <img  v-if="leftTeamChoice ==='Rock'" src="/src/assets/img/RockF.png" alt="Rock">
                    <img  v-if="leftTeamChoice ==='Paper'" src="/src/assets/img/PaperF.png" alt="Paper">
                    <img  v-if="leftTeamChoice ==='Scissors'" src="/src/assets/img/ScissorF.png" alt="Scissors">
                    <img  v-if="leftTeamChoice ==='Love'" src="/src/assets/img/LoveF.png" alt="Love">
                </div>
            <p>Left</p>
            </div>
        </div>
        <div class="team">
            <div class="team-info">
                <div class="imgframe">
                    <img v-if="rightTeamChoice ===''" src="/src/assets/img/ScissorF.png" alt="Scissors">
                    <img v-if="rightTeamChoice ==='Rock'" src="/src/assets/img/RockF.png" alt="Rock">
                    <img v-if="rightTeamChoice ==='Paper'" src="/src/assets/img/PaperF.png" alt="Paper">
                    <img v-if="rightTeamChoice ==='Scissors'" src="/src/assets/img/ScissorF.png" alt="Scissors">
                    <img v-if="rightTeamChoice ==='Love'" src="/src/assets/img/LoveF.png" alt="Love">
                </div>
            <p>Right</p>
            </div>
        </div>
        </div>
       
        <div class="result">
            <p>{{ gameResult }}</p>
        </div>
        <div class="button-container">
            <button class="playbutton" @click="playGame">Play</button>
            <button class="resetbutton" @click="resetGame">Reset</button>
        </div>
    </div>
        <div class="heartcontainner">
            <div class="heartframe">
                    <div class="heart" v-if="leftTeamChoice === 'Love' || rightTeamChoice === 'Love'">
                        YmY Heart
                    </div>
            </div>
    </div>
</div>

<footer>
    @Thonthus Prangpetch 6504101343
</footer>

</template>

<script>
export default {
  data() {
    return {
      leftTeamChoice: '',
      rightTeamChoice: '',
      gameResult: "Let's Play!!!",
      leftScore: 0,
      rightScore: 0,
      round: 0, 
    };
  },
  methods: {
    playGame() {
      
      const choices = ['Rock', 'Paper', 'Scissors', 'Love'];

      
      this.leftTeamChoice = choices[Math.floor(Math.random() * 3) + 1];
      this.rightTeamChoice = choices[Math.floor(Math.random() * 3) + 1];


      

     
      if (this.leftTeamChoice === 'Love' || this.rightTeamChoice === 'Love') {
        if (this.leftTeamChoice === 'Love' && this.rightTeamChoice === 'Love') {
        this.gameResult = 'Tie';
        }
        else if (this.leftTeamChoice === 'Love') {
          this.gameResult = 'Left Wins with Love!';
          this.leftScore++;
        } else {
          this.gameResult = 'Right Wins with Love!';
          this.rightScore++;
        }
      } else if (this.leftTeamChoice === this.rightTeamChoice) { 
        this.gameResult = 'Tie';
      } else if (
        (this.leftTeamChoice === 'Rock' && this.rightTeamChoice === 'Scissors') ||
        (this.leftTeamChoice === 'Paper' && this.rightTeamChoice === 'Rock') ||
        (this.leftTeamChoice === 'Scissors' && this.rightTeamChoice === 'Paper')
      ) {
        this.gameResult = 'Left Wins!!!';
        this.leftScore++;
      } else {
        this.gameResult = 'Right Wins!!!';
        this.rightScore++;
      }
      this.round++;
    },
    resetGame() {
      this.leftTeamChoice = '';
      this.rightTeamChoice = '';
      this.leftTeamChoiceImg = '';
      this.rightTeamChoiceImg = '';
      this.gameResult = "Let's Play!!!";
      this.leftScore = 0;
      this.rightScore = 0;
      this.round = 0;
    },
  },
    computed: {
        scoreboardMessage() {
            const leftPointsText = this.leftScore === 1 ? 'point' : (this.leftScore === 0 ? 'point' : 'points');
            const rightPointsText = this.rightScore === 1 ? 'point' : (this.rightScore === 0 ? 'point' : 'points');
        return `Left ${this.leftScore} ${leftPointsText} : Right ${this.rightScore} ${rightPointsText}`;
        },
        roundMessage() {
        
        if (this.round === 0) {
            return 'Click Play To Start';
        } else {
            return `Round ${this.round}`;
        }
        },
    },
};
</script>

<style scoped>
 
</style>
