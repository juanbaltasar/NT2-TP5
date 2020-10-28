<template>
    <div id="app">
        <div id="header">
            <h1>
                The Great <br>
                <span id="colorDisplay">{{ColorWinner}}</span>
                <br>
                Guessing Game
            </h1>
        </div>

        <div id="navigator">
            <button id="reset" @click="Restart"> {{TextoRestart}} </button>
            <span id="message">{{ message }}</span>

            <button id="easy" :class="{ selected:EasyMode }" @click="Easy()">easy</button>
            <button id="hard" :class="{ selected:!EasyMode }" @click="Difficult()">hard</button>
        </div>
        <Square v-for="item in getSquareData" :key="item.Id" :item="item" @squareClick="SquareClick"/>
    </div>
</template>

<script>
import Square from './components/Square.vue';

export default {
  name: 'App',
  components: {
    Square
  },
  data: () => {
        return({Victory: false,
        IdWinner: 0,
        ColorWinner: '',
        EasyMode: false,
        SquaresData:[],
        message:''})
    },

    mounted() {
        this.initSquares();
    },

    computed: {

        TextoRestart() {
            if (this.Victory) {
                return "Play Again!";
            } else {
                return "New Colors";
            }
        },

        getSquareData() {
            return this.SquaresData;
        },

        // SquareData() {
        //     this.SquaresData = []
        //     if (!this.Victory) {
        //         this.IdWinner = Math.floor(Math.random() * 3);
        //         for (let i = 0; i < (this.EasyMode ? 3 : 6); i++) {
        //             if (i === this.IdWinner) {
        //                 this.ColorWinner = this.createRandomStringColor();
        //                 this.SquaresData.push({
        //                     Id: i,
        //                     Color: this.ColorWinner,
        //                     Victory:false,
        //                     clicked:false
        //                 });
        //             } else {
        //                 this.SquaresData.push({
        //                     Id: i,
        //                     Color: this.createRandomStringColor(),
        //                     Victory:false,
        //                     clicked:false
        //                 })
        //             }
        //         }
        //     } else {
        //         for (let i = 0; i < (this.EasyMode ? 3 : 6); i++) {
        //             this.SquaresData.push({
        //                 Id: i,
        //                 Color: this.ColorWinner,
        //                 Victory:true,
        //                 clicked:false
        //             })
        //         }
        //     }
        //     return this.SquaresData;
        // }
    },

    methods: {
        initSquares(){
            this.message = '';
            this.SquaresData = []
            this.IdWinner = Math.floor(Math.random() * (this.EasyMode ? 3 : 6));
                for (let i = 0; i < (this.EasyMode ? 3 : 6); i++) {
                    if (i === this.IdWinner) {
                        this.ColorWinner = this.createRandomStringColor();
                        this.SquaresData.push({
                            Id: i,
                            Color: this.ColorWinner,
                            Victory:false,
                            clicked:false
                        });
                    } else {
                        this.SquaresData.push({
                            Id: i,
                            Color: this.createRandomStringColor(),
                            Victory:false,
                            clicked:false
                        })
                    }
                }
        },

        SquareClick(event) {
            if (!this.Victory) {
                if (event.IdSquare === this.IdWinner) {
                    this.Victory = true;
                    this.message = 'You won!'
                    for (const Square of this.SquaresData) {
                        Square.Victory = true;
                        Square.clicked = false;
                        Square.Color=this.ColorWinner;
                    }
                } else{
                    this.message = 'Try Again!'
                    this.SquaresData[event.IdSquare].clicked = true;
                }
            }
        },

        randomInt() {
            return Math.floor(Math.random() * 256);
        },

        createRandomStringColor() {
            var newColor = "rgb(" + this.randomInt() + "," + this.randomInt() + "," + this.randomInt() + ")";
            //	console.log(newColor);
            return newColor;
        },

        Restart() {
            this.Victory = false;
            this.initSquares();
        },

        Easy() {
            this.EasyMode = true;
        },

        Difficult() {
            this.EasyMode = false;
        }
    }
}
</script>

<style>
.Square{
    width: 30%;
	background: blue;
	padding-bottom: 30%;
	float: left;
	margin: 1.66%;
	border-radius: 10%;
	transition: background 0.8s;
	-webkit-transition: background 0.8s;
	-moz-transition: background 0.8s;
}
.hidden{
	width: 10rem;
	height: 10rem;
	visibility: hidden;
}
body {
	background: #232323;
	margin: 0;
	font-family: "Montserrat", "Avenir";
}

h1 {
	font-weight: normal;
	line-height: 1.1;
	padding: 20px 0;

}
#navigator {

	background: #ffffff;
	height: 30px;
	text-align: center;
	margin: 0;
	margin-top: -30px;

}
#header {
	transition: all 0.3s;
	background: steelblue;
	text-transform: uppercase;
	text-align: center;
	margin: 0;
	color: white;
	
}
#colorDisplay {
	font-size: 200%;
}


/* .square {
	width: 30%;
	background: blue;
	padding-bottom: 30%;
	float: left;
	margin: 1.66%;
	border-radius: 10%;
	transition: background 0.8s;
	-webkit-transition: background 0.8s;
	-moz-transition: background 0.8s;

} */
#container {
	margin: 20px auto;
	max-width: 600px;
}
#message {
	color: #000040;
	display: inline-block;
	width: 20%;
}

#messageBox {
	
}
.selected {
	background-color: steelblue;
	color: white;
}
button {
	border: none;
	background-color: white;
	font-family: "Montserrat", "Avenir";
	text-transform: uppercase;
	height: 100%;
	font-weight: 700;
	letter-spacing: 1px;
	color: steelblue;
	transition: all 0.3s;
	outline: none;
}
button:hover {
	color: white;
	background-color: steelblue;
}
</style>
