<template>
  <div>
    <div class="flex">
      <a class="title">Tic Tac Toe</a>
    </div>
    <div class="flex noMargin">
      <p v-if="winner === false" id="whose" class="left">
        It's <b>{{ whosTurn }}</b
        >'s turn.
      </p>
      <p class="left score">Score:</p>
      <p class="score left"><b>X:</b> {{ xWins }}</p>
      <p class="score left"><b>O:</b> {{ yWins }}</p>
      <!-- <p class="score left"><b>Turn: </b>{{ turn }}</p> -->
    </div>
    <p v-if="cat" class="winner">{{ cat }}</p>
    <p v-if="winner" class="winner">{{ winner }}</p>
    <div id="holdDoOver">
      <button emote class="btn" @click="doOver">New Game</button>

      <button class="rbtn" @click="restart">Reset Score</button>
    </div>
    <div class="outer">
      <div class="top">
        <table>
          <tr>
            <td id="x1" :class="{ show: showX1, hide: hideX1 }">X</td>
            <td id="x2" :class="{ show: showX2, hide: hideX2 }">X</td>
            <td id="x3" :class="{ show: showX3, hide: hideX3 }">X</td>
          </tr>
          <tr>
            <td id="x4" :class="{ show: showX4, hide: hideX4 }">X</td>
            <td id="x5" :class="{ show: showX5, hide: hideX5 }">X</td>
            <td id="x6" :class="{ show: showX6, hide: hideX6 }">X</td>
          </tr>
          <tr>
            <td id="x7" :class="{ show: showX7, hide: hideX7 }">X</td>
            <td id="x8" :class="{ show: showX8, hide: hideX8 }">X</td>
            <td id="x9" :class="{ show: showX9, hide: hideX9 }">X</td>
          </tr>
        </table>
      </div>
      <div class="bottom">
        <table>
          <tr>
            <td id="y1" :class="{ showY: showY1, hide: hideY1 }">O</td>
            <td id="y2" :class="{ showY: showY2, hide: hideY2 }">O</td>
            <td id="y3" :class="{ showY: showY3, hide: hideY3 }">O</td>
          </tr>
          <tr>
            <td id="y4" :class="{ showY: showY4, hide: hideY4 }">O</td>
            <td id="y5" :class="{ showY: showY5, hide: hideY5 }">O</td>
            <td id="y6" :class="{ showY: showY6, hide: hideY6 }">O</td>
          </tr>
          <tr>
            <td id="y7" :class="{ showY: showY7, hide: hideY7 }">O</td>
            <td id="y8" :class="{ showY: showY8, hide: hideY8 }">O</td>
            <td id="y9" :class="{ showY: showY9, hide: hideY9 }">O</td>
          </tr>
        </table>
      </div>
      <div class="top2" v-if="whosTurn === 'X'">
        <table>
          <tr>
            <td class="p" id="p1" @click="placeX1">p</td>
            <td class="p" id="p2" @click="placeX2">p</td>
            <td class="p" id="p3" @click="placeX3">p</td>
          </tr>
          <tr>
            <td class="p" id="p4" @click="placeX4">p</td>
            <td class="p" id="p5" @click="placeX5">p</td>
            <td class="p" id="p6" @click="placeX6">p</td>
          </tr>
          <tr>
            <td class="p" id="p7" @click="placeX7">p</td>
            <td class="p" id="p8" @click="placeX8">p</td>
            <td class="p" id="p9" @click="placeX9">p</td>
          </tr>
        </table>
      </div>
      <div class="top3" v-if="whosTurn === 'O'">
        <table>
          <tr>
            <td class="q" id="q10" @click="placeY1">q</td>
            <td class="q" id="q11" @click="placeY2">q</td>
            <td class="q" id="q12" @click="placeY3">q</td>
          </tr>
          <tr>
            <td class="q" id="q13" @click="placeY4">q</td>
            <td class="q" id="q14" @click="placeY5">q</td>
            <td class="q" id="q15" @click="placeY6">q</td>
          </tr>
          <tr>
            <td class="q" id="q16" @click="placeY7">q</td>
            <td class="q" id="q17" @click="placeY8">q</td>
            <td class="q" id="q18" @click="placeY9">q</td>
          </tr>
        </table>
      </div>
      <div class="below">
        <table>
          <tr>
            <td class="white" id="q10">q</td>
            <td class="white" id="q11">q</td>
            <td class="white" id="q12">q</td>
          </tr>
          <tr>
            <td class="white" id="q13">q</td>
            <td class="white" id="q14">q</td>
            <td class="white" id="q15">q</td>
          </tr>
          <tr>
            <td class="white" id="q16">q</td>
            <td class="white" id="q17">q</td>
            <td class="white" id="q18">q</td>
          </tr>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    var audio = new Audio(require("@/assets/click.mp3"));
    var meow = new Audio(require("@/assets/meow.mp3"));
    var bell = new Audio(require("@/assets/bell.mp3"));
    var turn = 0;
    var cat = false;
    var btn = false;
    var winner = false;
    var xWins = 0;
    var yWins = 0;
    var whosTurn = "X";
    var showX1 = false;
    var showX2 = false;
    var showX3 = false;
    var showX4 = false;
    var showX5 = false;
    var showX6 = false;
    var showX7 = false;
    var showX8 = false;
    var showX9 = false;
    var showY1 = false;
    var showY2 = false;
    var showY3 = false;
    var showY4 = false;
    var showY5 = false;
    var showY6 = false;
    var showY7 = false;
    var showY8 = false;
    var showY9 = false;
    var hideX1 = true;
    var hideX2 = true;
    var hideX3 = true;
    var hideX4 = true;
    var hideX5 = true;
    var hideX6 = true;
    var hideX7 = true;
    var hideX8 = true;
    var hideX9 = true;
    var hideY1 = true;
    var hideY2 = true;
    var hideY3 = true;
    var hideY4 = true;
    var hideY5 = true;
    var hideY6 = true;
    var hideY7 = true;
    var hideY8 = true;
    var hideY9 = true;

    return {
      audio,
      meow,
      bell,
      cat,
      turn,
      btn,
      winner,
      xWins,
      yWins,
      whosTurn,
      showX1,
      showX2,
      showX3,
      showX4,
      showX5,
      showX6,
      showX7,
      showX8,
      showX9,
      showY1,
      showY2,
      showY3,
      showY4,
      showY5,
      showY6,
      showY7,
      showY8,
      showY9,
      hideX1,
      hideX2,
      hideX3,
      hideX3,
      hideX4,
      hideX5,
      hideX6,
      hideX7,
      hideX8,
      hideX9,
      hideY1,
      hideY2,
      hideY3,
      hideY4,
      hideY5,
      hideY6,
      hideY7,
      hideY8,
      hideY9,
    };
  },
  methods: {
    click() {
      this.audio.play();
    },
    win() {
      this.bell.play();
    },
    catgame() {
      this.meow.play();
    },
    // restart
    doOver() {
      this.turn = 0;
      this.cat = false;
      this.btn = false;
      this.whosTurn = "X";
      this.winner = false;
      this.hideX1 = true;
      this.hideX2 = true;
      this.hideX3 = true;
      this.hideX4 = true;
      this.hideX5 = true;
      this.hideX6 = true;
      this.hideX7 = true;
      this.hideX8 = true;
      this.hideX9 = true;
      this.hideY1 = true;
      this.hideY2 = true;
      this.hideY3 = true;
      this.hideY4 = true;
      this.hideY5 = true;
      this.hideY6 = true;
      this.hideY7 = true;
      this.hideY8 = true;
      this.hideY9 = true;
      this.showX1 = false;
      this.showX2 = false;
      this.showX3 = false;
      this.showX4 = false;
      this.showX5 = false;
      this.showX6 = false;
      this.showX7 = false;
      this.showX8 = false;
      this.showX9 = false;
      this.showY1 = false;
      this.showY2 = false;
      this.showY3 = false;
      this.showY4 = false;
      this.showY5 = false;
      this.showY6 = false;
      this.showY7 = false;
      this.showY8 = false;
      this.showY9 = false;

      window.scrollTo(0, 1000);
    },
    // turn designation
    xTurn() {
      console.log("Now it's X's turn");
      this.whosTurn = "X";
    },
    yTurn() {
      console.log("Now it's O's turn");
      this.whosTurn = "O";
    },

    // The squares/turns VVV
    // X's turns
    placeX1() {
      if (this.whosTurn === "X") {
        if (this.showY1 === false && this.showX1 === false) {
          console.log("X placed on 1");
          this.hideX1 = false;
          this.showX1 = true;
          this.turn++;

          this.click();
          this.yTurn();
        }
        // 1,2,3
        if (
          this.showX1 === true &&
          this.showX2 === true &&
          this.showX3 === true
        ) {
          this.winner = "X Wins!";
          this.win();
          console.log(this.xWins);

          ++this.xWins;
          this.btn = true;

          console.log(this.xWins);
          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        // 1,5,9
        if (
          this.showX1 === true &&
          this.showX5 === true &&
          this.showX9 === true
        ) {
          console.log(this.xWins);
          this.winner = "X Wins!!!";
          this.win();
          ++this.xWins;
          window.scrollTo(0, 0);
          this.btn = true;
          console.log("X wins");
        }
        // 1,4,7
        if (
          this.showX1 === true &&
          this.showX4 === true &&
          this.showX7 === true
        ) {
          this.winner = "X Wins!";
          this.win();
          console.log(this.xWins);

          ++this.xWins;
          this.btn = true;

          console.log(this.xWins);
          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        if (this.turn === 9 && this.winner === false) {
          this.cat = "Cat's Game";
          this.catgame();
        }
      } // END whoseTurn if statement
    }, // END PlaceX1
    placeX2() {
      if (this.whosTurn === "X") {
        if (this.showY2 === false && this.showX2 === false) {
          console.log("X placed on 2");
          this.hideX2 = false;
          this.showX2 = true;
          this.turn++;

          this.click();
          this.yTurn();
        }
        // 1,2,3
        if (
          this.showX1 === true &&
          this.showX2 === true &&
          this.showX3 === true
        ) {
          this.winner = "X Wins!";
          this.win();
          console.log(this.xWins);

          ++this.xWins;
          this.btn = true;

          console.log(this.xWins);
          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        // 2,5,8
        if (
          this.showX2 === true &&
          this.showX5 === true &&
          this.showX8 === true
        ) {
          this.winner = "X Wins!";
          this.win();
          console.log(this.xWins);

          ++this.xWins;
          this.btn = true;

          console.log(this.xWins);
          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        if (this.turn === 9 && this.winner === false) {
          this.cat = "Cat's Game";
          this.catgame();
        }
      } // END whoseTurn if statement
    }, // END PlaceX2
    placeX3() {
      if (this.whosTurn === "X") {
        if (this.showY3 === false && this.showX3 === false) {
          console.log("X placed on 3");
          this.hideX3 = false;
          this.showX3 = true;
          this.turn++;

          this.click();
          this.yTurn();
        }
        if (
          this.showX1 === true &&
          this.showX2 === true &&
          this.showX3 === true
        ) {
          this.winner = "X Wins!";
          this.win();
          console.log(this.xWins);

          ++this.xWins;
          this.btn = true;

          console.log(this.xWins);
          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        if (
          this.showX3 === true &&
          this.showX6 === true &&
          this.showX9 === true
        ) {
          this.winner = "X Wins!";
          this.win();
          console.log(this.xWins);

          ++this.xWins;
          this.btn = true;

          console.log(this.xWins);
          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        if (
          this.showX3 === true &&
          this.showX5 === true &&
          this.showX7 === true
        ) {
          this.winner = "X Wins!";
          console.log(this.xWins);
          this.win();
          ++this.xWins;
          this.btn = true;

          console.log(this.xWins);
          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        if (this.turn === 9 && this.winner === false) {
          this.cat = "Cat's Game";
          this.catgame();
        }
      }
    },
    placeX4() {
      if (this.whosTurn === "X") {
        if (this.showY4 === false && this.showX4 === false) {
          console.log("X placed on 4");
          this.hideX4 = false;
          this.showX4 = true;
          this.turn++;

          this.click();
          this.yTurn();
        }
        if (
          this.showX4 === true &&
          this.showX5 === true &&
          this.showX6 === true
        ) {
          this.winner = "X Wins!";
          this.win();
          console.log(this.xWins);

          ++this.xWins;
          this.btn = true;

          console.log(this.xWins);
          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        if (
          this.showX1 === true &&
          this.showX4 === true &&
          this.showX7 === true
        ) {
          this.winner = "X Wins!";
          this.win();
          console.log(this.xWins);

          ++this.xWins;
          this.btn = true;

          console.log(this.xWins);
          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        if (this.turn === 9 && this.winner === false) {
          this.cat = "Cat's Game";
          this.catgame();
        }
      }
    },
    placeX5() {
      if (this.whosTurn === "X") {
        if (this.showY5 === false && this.showX5 === false) {
          console.log("X placed on 5");
          this.hideX5 = false;
          this.showX5 = true;
          this.turn++;

          this.click();
          this.yTurn();
        }
        // 1,5,9
        if (
          this.showX1 === true &&
          this.showX5 === true &&
          this.showX9 === true
        ) {
          console.log(this.xWins);
          this.winner = "X Wins!";
          this.win();
          ++this.xWins;
          window.scrollTo(0, 0);
          this.btn = true;
          console.log("X wins");
        }
        // 3,5,7
        if (
          this.showX3 === true &&
          this.showX5 === true &&
          this.showX7 === true
        ) {
          console.log(this.xWins);
          this.winner = "X Wins!";
          this.win();
          ++this.xWins;
          window.scrollTo(0, 0);
          this.btn = true;
          console.log("X wins");
        }
        // 4,5,6
        if (
          this.showX4 === true &&
          this.showX5 === true &&
          this.showX6 === true
        ) {
          console.log(this.xWins);
          this.winner = "X Wins!";
          this.win();
          ++this.xWins;
          window.scrollTo(0, 0);
          this.btn = true;
          console.log("X wins");
        }
        if (this.turn === 9 && this.winner === false) {
          this.cat = "Cat's Game";
          this.catgame();
        }
      } // END If statement
    }, // END placeX5
    placeX6() {
      if (this.whosTurn === "X") {
        if (this.showY6 === false && this.showX6 === false) {
          console.log("X placed on 6");
          this.hideX6 = false;
          this.showX6 = true;
          this.turn++;

          this.click();
          this.yTurn();
        }
        // 4,5,6
        if (
          this.showX4 === true &&
          this.showX5 === true &&
          this.showX6 === true
        ) {
          console.log(this.xWins);
          this.winner = "X Wins!";
          this.win();
          ++this.xWins;
          window.scrollTo(0, 0);
          this.btn = true;
          console.log("X wins");
        }
        // 3,6,9
        if (
          this.showX3 === true &&
          this.showX6 === true &&
          this.showX9 === true
        ) {
          console.log(this.xWins);
          this.winner = "X Wins!";
          this.win();
          ++this.xWins;
          window.scrollTo(0, 0);
          this.btn = true;
          console.log("X wins");
        }
        if (this.turn === 9 && this.winner === false) {
          this.cat = "Cat's Game";
          this.catgame();
        }
      }
    },
    placeX7() {
      if (this.whosTurn === "X") {
        if (this.showY7 === false && this.showX7 === false) {
          console.log("X placed on 7");
          this.hideX7 = false;
          this.showX7 = true;
          this.turn++;

          this.click();
          this.yTurn();
        }
        // 1,4,7
        if (
          this.showX1 === true &&
          this.showX4 === true &&
          this.showX7 === true
        ) {
          console.log(this.xWins);
          this.winner = "X Wins!";
          this.win();
          ++this.xWins;
          window.scrollTo(0, 0);
          this.btn = true;
          console.log("X wins");
        }
        // 3,5,7
        if (
          this.showX3 === true &&
          this.showX5 === true &&
          this.showX7 === true
        ) {
          console.log(this.xWins);
          this.winner = "X Wins!";
          this.win();
          ++this.xWins;
          window.scrollTo(0, 0);
          this.btn = true;
          console.log("X wins");
        }
        if (this.turn === 9 && this.winner === false) {
          this.cat = "Cat's Game";
          this.catgame();
        }
      }
    },
    placeX8() {
      if (this.whosTurn === "X") {
        if (this.showY8 === false && this.showX8 === false) {
          console.log("X placed on 1");
          this.hideX8 = false;
          this.showX8 = true;
          this.turn++;

          this.click();
          this.yTurn();
        }
        // ,5,8
        if (
          this.showX2 === true &&
          this.showX5 === true &&
          this.showX8 === true
        ) {
          console.log(this.xWins);
          this.winner = "X Wins!";
          this.win();
          ++this.xWins;
          window.scrollTo(0, 0);
          this.btn = true;
          console.log("X wins");
        }
        // 7,8,9
        if (
          this.showX7 === true &&
          this.showX8 === true &&
          this.showX9 === true
        ) {
          console.log(this.xWins);
          this.winner = "X Wins!";
          this.win();
          ++this.xWins;
          window.scrollTo(0, 0);
          this.btn = true;
          console.log("X wins");
        }
        if (this.turn === 9 && this.winner === false) {
          this.cat = "Cat's Game";
          this.catgame();
        }
      }
    },
    placeX9() {
      if (this.whosTurn === "X") {
        if (this.showY9 === false && this.showX9 === false) {
          console.log("X placed on 9");
          this.hideX9 = false;
          this.showX9 = true;
          this.turn++;

          this.click();
          this.yTurn();
        }
        // 1,5,9
        if (
          this.showX1 === true &&
          this.showX5 === true &&
          this.showX9 === true
        ) {
          console.log(this.xWins);
          this.winner = "X Wins!";
          this.win();
          ++this.xWins;
          window.scrollTo(0, 0);
          this.btn = true;
          console.log("X wins");
        }
        // 3,6,9
        if (
          this.showX3 === true &&
          this.showX6 === true &&
          this.showX9 === true
        ) {
          console.log(this.xWins);
          this.winner = "X Wins!";
          this.win();
          ++this.xWins;
          window.scrollTo(0, 0);
          this.btn = true;
          console.log("X wins");
        }
        // 7,8,9
        if (
          this.showX7 === true &&
          this.showX8 === true &&
          this.showX9 === true
        ) {
          console.log(this.xWins);
          this.winner = "X Wins!";
          this.win();
          ++this.xWins;
          window.scrollTo(0, 0);
          this.btn = true;
          console.log("X wins");
        }
        if (this.turn === 9 && this.winner === false) {
          this.cat = "Cat's Game";
          this.catgame();
        }
      }
    },
    // Y's turns
    placeY1() {
      if (this.whosTurn === "O") {
        if (this.showY1 === false && this.showX1 === false) {
          console.log("O placed on 1");
          this.hideY1 = false;
          this.showY1 = true;
          this.turn++;
          if (this.turn === 9 && this.winner === false) {
            this.cat = "Cat's Game";
          }
          this.click();
          this.xTurn();
        }
        // LEFT OFF HERE 5/9
        // 1,2,3
        if (
          this.showY1 === true &&
          this.showY2 === true &&
          this.showY3 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        // 1,5,9
        if (
          this.showY1 === true &&
          this.showY5 === true &&
          this.showY9 === true
        ) {
          console.log(this.yWins);
          this.winner = "O Wins!!!";
          this.win();
          ++this.yWins;
          window.scrollTo(0, 0);
          this.btn = true;
        }
        // 1,4,7
        if (
          this.showY1 === true &&
          this.showY4 === true &&
          this.showY7 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        this.xTurn();
        if (this.turn === 9 && this.winner === false) {
          this.cat = "Cat's Game";
          this.catgame();
        }
      }
    },
    placeY2() {
      if (this.whosTurn === "O") {
        if (this.showY2 === false && this.showX2 === false) {
          console.log("O placed on 2");
          this.hideY2 = false;
          this.showY2 = true;
          this.turn++;

          this.click();
          this.xTurn();
        }
        // 2,5,8
        if (
          this.showY2 === true &&
          this.showY5 === true &&
          this.showY8 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        if (this.turn === 9 && this.winner === false) {
          this.cat = "Cat's Game";
          this.catgame();
        }
      }
    },
    placeY3() {
      if (this.whosTurn === "O") {
        if (this.showY3 === false && this.showX3 === false) {
          console.log("O placed on 3");
          this.hideY3 = false;
          this.showY3 = true;
          this.turn++;

          this.click();
          this.xTurn();
        }
        // 1,2,3
        if (
          this.showY1 === true &&
          this.showY2 === true &&
          this.showY3 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        // 3,5,7
        if (
          this.showY3 === true &&
          this.showY5 === true &&
          this.showY7 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        // 3,6,9
        if (
          this.showY3 === true &&
          this.showY6 === true &&
          this.showY9 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        if (this.turn === 9 && this.winner === false) {
          this.cat = "Cat's Game";
          this.catgame();
        }
      }
    },
    placeY4() {
      if (this.whosTurn === "O") {
        if (this.showX4 === false && this.showY4 === false) {
          console.log("O placed on 4");
          this.hideY4 = false;
          this.showY4 = true;
          this.turn++;

          this.click();
          this.xTurn();
        }
        // 1,4,7
        if (
          this.showY1 === true &&
          this.showY4 === true &&
          this.showY7 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        // 4,5,6
        if (
          this.showY4 === true &&
          this.showY5 === true &&
          this.showY6 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        if (this.turn === 9 && this.winner === false) {
          this.cat = "Cat's Game";
          this.catgame();
        }
        this.xTurn();
      }
    },
    placeY5() {
      if (this.whosTurn === "O") {
        if (this.showX5 === false && this.showY5 === false) {
          console.log("O placed on 5");
          this.hideY5 = false;
          this.showY5 = true;
          this.turn++;

          this.click();
          this.xTurn();
        }
        // 1,5,9
        if (
          this.showY1 === true &&
          this.showY5 === true &&
          this.showY9 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        // 4,5,6
        if (
          this.showY4 === true &&
          this.showY5 === true &&
          this.showY6 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        // 3,5,7
        if (
          this.showY3 === true &&
          this.showY5 === true &&
          this.showY7 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        if (this.turn === 9 && this.winner === false) {
          this.cat = "Cat's Game";
          this.catgame();
        }
        this.xTurn();
      }
    },
    placeY6() {
      if (this.whosTurn === "O") {
        if (this.showX6 === false && this.showY6 === false) {
          console.log("O placed on 6");
          this.hideY6 = false;
          this.showY6 = true;
          this.turn++;

          this.click();
          this.xTurn();
        }
        // 4,5,6
        if (
          this.showY4 === true &&
          this.showY5 === true &&
          this.showY6 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        // 3,6,9
        if (
          this.showY3 === true &&
          this.showY6 === true &&
          this.showY9 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        if (this.turn === 9 && this.winner === false) {
          this.cat = "Cat's Game";
          this.catgame();
        }
        this.xTurn();
      }
    },
    placeY7() {
      if (this.whosTurn === "O") {
        if (this.showX7 === false && this.showY7 === false) {
          console.log("O placed on 7");
          this.hideY7 = false;
          this.showY7 = true;
          this.turn++;

          this.click();
          this.xTurn();
        }
        // 1,4,7
        if (
          this.showY1 === true &&
          this.showY4 === true &&
          this.showY7 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        // 3,5,7
        if (
          this.showY3 === true &&
          this.showY5 === true &&
          this.showY7 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        // 7,8,9
        if (
          this.showY7 === true &&
          this.showY8 === true &&
          this.showY9 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        if (this.turn === 9 && this.winner === false) {
          this.cat = "Cat's Game";
          this.catgame();
        }
        this.xTurn();
      }
    },
    placeY8() {
      if (this.whosTurn === "O") {
        if (this.showX8 === false && this.showY8 === false) {
          console.log("O placed on 8");
          this.hideY8 = false;
          this.showY8 = true;
          this.turn++;

          this.click();
          this.xTurn();
        }
        // 2,5,8
        if (
          this.showY2 === true &&
          this.showY5 === true &&
          this.showY8 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        // 7,8,9
        if (
          this.showY7 === true &&
          this.showY8 === true &&
          this.showY9 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }

        if (this.turn === 9 && this.winner === false) {
          this.cat = "Cat's Game";
          this.catgame();
        }
        this.xTurn();
      }
    },
    placeY9() {
      if (this.whosTurn === "O") {
        if (this.showX9 === false && this.showY9 === false) {
          console.log("O placed on 9");
          this.hideY9 = false;
          this.showY9 = true;
          this.turn++;

          this.click();
          this.xTurn();
        }
        // 1,5,9
        if (
          this.showY1 === true &&
          this.showY5 === true &&
          this.showY9 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        // 3,6,9
        if (
          this.showY3 === true &&
          this.showY6 === true &&
          this.showY9 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        } // 7,8,9
        if (
          this.showY7 === true &&
          this.showY8 === true &&
          this.showY9 === true
        ) {
          this.winner = "O Wins!";
          this.win();
          console.log(this.yWins);

          ++this.yWins;
          this.btn = true;

          window.scrollTo(0, 0);
          this.btn = true;
          console.log(this.winner);
        }
        if (this.turn === 9 && this.winner === false) {
          this.cat = "Cat's Game";
          this.catgame();
        }
        this.xTurn();
      }
    },
    restart() {
      window.scrollTo(0, 1000);
      location.reload();
    },
  },
};
</script>

<style>
body {
  width: 100%;
  background: whitesmoke;
}
table {
  margin-right: auto;
  margin-left: auto;
  width: 33%;
  height: 33em;
}
table,
td {
  border: 1px solid black;
  border-collapse: collapse;
}
td {
  width: 33em;
  height: 33%;
  position: relative;
  font-size: 5em;
  font-weight: 600;
}
.btn {
  margin: 1em;
  border: none;
  background: powderblue;
  border-radius: 5px;
  box-shadow: 1px 2px 3px rgb(7, 7, 7, 0.5);
}
.rbtn {
  margin: 1em;
  border: none;
  background: rgb(214, 102, 94);
  color: white;
  border-radius: 5px;
  box-shadow: 1px 2px 3px rgb(7, 7, 7, 0.5);
}
.outer {
  display: grid;
  grid-template: 1fr / 1fr;
  place-items: center;
}
.outer > * {
  grid-column: 1 / 1;
  grid-row: 1 / 1;
}
.outer .below {
  z-index: 0;
}
.outer .top {
  z-index: 1;
}
.top2,
.top3 {
  z-index: 3;
}
.below {
  color: rgb(0, 0, 0, 0);
  margin: 0;
  padding: 0;
}
h1 {
  margin: 0;
}
.flex {
  display: flex;
  justify-content: center;
}
.p,
.q {
  color: rgb(255, 255, 255, 0);
}
.show {
  color: green;
  background: none;
  z-index: 3;
}
.showY {
  color: rgb(128, 0, 100);
  background: none;
  z-index: 3;
}
.hide {
  color: white;
  background: none;
  z-index: -3;
}
#whose {
  font-size: 2em;
  margin: 0;
}
#holdDoOver {
  height: 1em;
  margin-bottom: 1em;
}
.title {
  font-size: 3em;
  font-family: monospace;
  font-weight: 600;
  margin-top: -1.5em;
  margin-bottom: 0;
}
.winner {
  font-size: 2.5em;
  font-family: Impact, Haettenschweiler, "Arial Narrow Bold", sans-serif;
  color: blue;
  margin: 0;
}
.left {
  float: left;
  margin-left: 0.5em;
}
.noMargin {
  margin: 0;
}
.score {
  font-size: 2em;
  margin: 0;
  margin-right: 0.5em;
}
#whose {
  margin-right: 0.5em;
}
.white {
  background: white;
}
</style>