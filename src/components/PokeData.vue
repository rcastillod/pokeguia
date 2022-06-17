<template>
	<div class="pokedex-wrapper">
		<div class="pokedex">
			<div class="left">
				<div class="bg_curve1_left"></div>
				<div class="bg_curve2_left"></div>
				<div class="curve1_left">
					<div class="glassBtn glassBtn--big glassBtn--lightblue">
						<div class="glassBtn__shadow"></div>
						<div class="glassBtn__middle"></div>
						<div class="glassBtn__shine"></div>
					</div>
					<div class="glassBtn glassBtn--red">
						<div class="glassBtn__shadow"></div>
						<div class="glassBtn__middle"></div>
						<div class="glassBtn__shine"></div>
					</div>
					<div class="glassBtn glassBtn--yellow">
						<div class="glassBtn__shadow"></div>
						<div class="glassBtn__middle"></div>
						<div class="glassBtn__shine"></div>
					</div>
					<div class="glassBtn glassBtn--green">
						<div class="glassBtn__shadow"></div>
						<div class="glassBtn__middle"></div>
						<div class="glassBtn__shine"></div>
					</div>
				</div>
				<div class="curve2_left">
					<div class="junction">
						<div class="junction1"></div>
						<div class="junction2"></div>
					</div>
				</div>
				<div class="screen">
					<div class="topPicture">
						<div class="buttontopPicture1"></div>
						<div class="buttontopPicture2"></div>
					</div>
					<div class="picture">
						<img :src="pokeImage" :alt="pokemon.name" />
					</div>
					<div class="bottomScreen-wrapper flex space-between">
						<div class="buttonbottomPicture"></div>
						<div class="speakers">
							<div class="sp"></div>
							<div class="sp"></div>
							<div class="sp"></div>
							<div class="sp"></div>
						</div>
					</div>
				</div>
				<div class="bigbluebutton"></div>
				<div class="barbutton1"></div>
				<div class="barbutton2"></div>
				<div class="cross">
					<div class="leftcross">
						<div class="leftT"></div>
					</div>
					<div class="topcross">
						<div class="upT"></div>
					</div>
					<div class="rightcross">
						<div class="rightT"></div>
					</div>
					<div class="midcross">
						<div class="midCircle"></div>
					</div>
					<div class="botcross">
						<div class="downT"></div>
					</div>
				</div>
			</div>
			<div class="right">
				<div class="stats">
					<div class="inputName flex align-center" style="--gap: .5rem">
						<label for="">Nombre:</label>
						<input class="inputName__input" type="text" v-model="pokemon.name" @keyup.enter="getPokeData" autofocus>
					</div>
					<div v-if="noresults" class="sinresultados">
						<p>No se encontraron resultados</p>
					</div>
					<div v-else>
						<div class="moves">
							<div class="moves__title">Movimientos</div>
							<div class="moves__horizontal-scroll">
								<p class="move" v-for="(move, index) in pokeMoves" :key="index">{{move}}</p>	
							</div>
						</div>
						<div class="abilities">
							<div class="abilities__title">Habilidades</div>
							<div class="abilities__horizontal-scroll">
								<p class="ability" v-for="(ability, index) in pokeAbilities" :key="index">{{ability}}</p>	
							</div>
						</div>
					</div>
				</div>
				<div class="blueButtons">
					<div class="blueButtons1">
						<div class="blueButton"></div>
						<div class="blueButton"></div>
						<div class="blueButton"></div>
						<div class="blueButton"></div>
						<div class="blueButton"></div>
					</div>
					<div class="blueButtons2">
						<div class="blueButton"></div>
						<div class="blueButton"></div>
						<div class="blueButton"></div>
						<div class="blueButton"></div>
						<div class="blueButton"></div>
					</div>
				</div>
				<div class="miniButtonGlass4"></div>
				<div class="miniButtonGlass5"></div>
				<div class="barbutton3"></div>
				<div class="barbutton4"></div>
				<div class="darkGreenBox1"></div>
				<div class="darkGreenBox2"></div>
				<div class="bg_curve1_right"></div>
				<div class="bg_curve2_right"></div>
				<div class="curve1_right"></div>
				<div class="curve2_right"></div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
    name: 'poke-data',
    // props: {},
    data: function(){
        return {
            pokemon: {
                name: 'pikachu',
                sprites: '',
                moves: [],
                abilities: []
            },
			noresults: false,
			noresultsImg: require('../assets/logo.png')
        }
    },
    computed: {
        pokeImage() {
            return this.pokemon.sprites.front_default
        },
        pokeAbilities() {
            let abilityArr = this.pokemon.abilities.map((ability) =>{
                return ability.ability.name
            })
            return abilityArr
        },
        pokeMoves() {
            let moveArr = this.pokemon.moves.map((move) =>{
                return move.move.name
            })
            return moveArr
        }
    },
    methods: {
        async getPokeData() {
            try {
                let response = await fetch(`https://pokeapi.co/api/v2/pokemon/${this.pokemon.name}`)
                if(!response.ok) throw ('Error en la petición de datos.')

                let results = await response.json()
                this.pokemon = results
				this.noresults = false
            }
            catch(error) {
				this.pokemon.sprites.front_default = this.noresultsImg
				this.noresults = true
                console.log(error)
            }
        }
    },
    // watch: {},
    // components: {},
    // mixins: [],
    // filters: {},
    // -- Lifecycle Methods
    created() {
        this.getPokeData()
    }
    // -- End Lifecycle Methods
}
</script>

<style scoped>
.pokedex {
	display: flex;
	width: 46.875rem;
}
.left {
	position: relative;
	height: 31.25rem;
	width: 25rem;
	z-index: 1;
}
.right {
	position: relative;
	height: 31.25rem;
	width: 21.875rem;
}

/* Left Panel */
.bg_curve1_left {
	background-color: var(--clr-body);
	border-top-left-radius: 1.875rem;
    border-top-right-radius: .9375rem;
	height: 5rem;
	width: 25rem;
}
.bg_curve2_left {
	background-color: var(--clr-body);
	border-bottom-left-radius: 1.875rem;
	box-shadow: 0px 9px var(--clr-body-shadow);
	height: 26.25rem;
	width: 25rem;
}
.curve1_left {
	background-color: var(--clr-body);
	border-bottom-right-radius: 30px;
	border-top-left-radius: 30px;
    box-shadow: 0px 9px var(--clr-body-shadow);
	display: flex;
	height: 5.3125rem;
	width: 13.1625rem;
	padding: .9375rem 0 0 .9375rem;
	position: absolute;
	top: 0;
	left: 0;
}
.curve2_left {
	background-color: var(--clr-body);
	border-top-left-radius: 25px;
	box-shadow: 0px -9px var(--clr-body-shadow);
	display: flex;
	justify-content: flex-end;
	height: 28.1875rem;
	width: 11.875rem;
	position: absolute;
	bottom: 0;
	right: 0;
}

.junction {
	background: linear-gradient(to left, #8b0000 0%, #c00d0d 50%, #8b0000 100%);
	height: 28.1875rem;
	width: 3.75rem;
}
.junction1 {
	background-color: var(--clr-body-shadow);
	border-bottom: 2px solid #330000;
	border-top: 2px solid #330000;
	height: 2.5rem;
	margin-top: 3.125rem;
	margin-bottom: 16.375rem;
	opacity: 0.3;
}
.junction2 {
	background-color: var(--clr-body-shadow);
	border-bottom: 2px solid #330000;
	border-top: 2px solid #330000;
	height: 2.5rem;
	opacity: 0.3;
}

.glassBtn {
	border: 2px solid var(--clr-border-grey);
	border-radius: 50%;
	display: grid;
	grid-template-columns: repeat(7, 1fr);
	grid-template-rows: repeat(7, 1fr);
	height: 1.25rem;
	width: 1.25rem;
	margin-right: 15px;
	outline: 1px solid var(--clr-button-darkgreen);
}
.glassBtn > * {
	border-radius: inherit;
	position: relative;
}
.glassBtn .glassBtn__shadow {
	grid-column: 2 / -1;
    grid-row: 2 / -1;
}
.glassBtn .glassBtn__middle {
	grid-column: 2 / 5;
    grid-row: 2 / 5;
	left: 1px;
	top: 1px;
}
.glassBtn .glassBtn__shine {
	grid-column: 2 / 3;
    grid-row: 2 / 3;
	left: 2px;
	top: 2px;
}
.glassBtn--big {
	border: 5px solid var(--clr-border-grey);
	width: 3.75rem;
	height: 3.75rem;
}
.glassBtn--big .glassBtn__middle {
	left: 2px;
	top: 2px;
}
.glassBtn--big .glassBtn__shine {
	left: 6px;
	top: 6px;
}

.glassBtn--lightblue {
	background-color: var(--clr-button-lightblue);
}
.glassBtn--lightblue .glassBtn__shadow {
	background-color: var(--clr-button-lightblue-shadow);
}
.glassBtn--lightblue .glassBtn__middle {
	background-color: var(--clr-button-lightblue);
}
.glassBtn--lightblue .glassBtn__shine {
	background-color: var(--clr-button-lightblue-shine);
}

.glassBtn--red {
	background-color: var(--clr-body);
}
.glassBtn--red .glassBtn__shadow {
	background-color: var(--clr-body-shadow);
}
.glassBtn--red .glassBtn__middle {
	background-color: var(--clr-body);
}
.glassBtn--red .glassBtn__shine {
	background-color: var(--clr-body-shine);
}

.glassBtn--yellow {
	background-color: var(--clr-button-yellow);
}
.glassBtn--yellow .glassBtn__shadow {
	background-color: var(--clr-button-yellow-shadow);
}
.glassBtn--yellow .glassBtn__middle {
	background-color: var(--clr-button-yellow);
}
.glassBtn--yellow .glassBtn__shine {
	background-color: var(--clr-button-yellow-shine);
}

.glassBtn--green {
	background-color: var(--clr-button-green);
}
.glassBtn--green .glassBtn__shadow {
	background-color: var(--clr-button-green-shadow);
}
.glassBtn--green .glassBtn__middle {
	background-color: var(--clr-button-green);
}
.glassBtn--green .glassBtn__shine {
	background-color: var(--clr-button-green-shine);
}

.screen {
	background-color: var(--clr-border-grey);
	border-radius: 15px;
	height: 15.3125rem;
	width: 18.4375rem;
	padding: 0 1.25rem;
	position: absolute;
	top: 130px;
	left: 19px;
}
.screen:after {
	content: "";
	border-left: 40px solid var(--clr-body);
	border-top: 40px solid var(--clr-border-grey);
	position: absolute;
	left: 0;
	bottom: 0;
}

.picture {
	border: 3px solid var(--clr-button-darkgreen);
	border-radius: 15px;
	display: grid;
	place-items: center;
	height: 10.9375rem;
	width: 15.875rem;
	margin-bottom: .5625rem;
	margin-top: .25rem;
	background-color: var(--clr-white);
}
.picture img {
	display: block;
	margin: 0 auto;
}
.topPicture {
	display: flex;
	gap: .625rem;
	margin: .375rem auto;
	width: 2.5rem;
}

.buttontopPicture1,
.buttontopPicture2 {
	background-color: var(--clr-body);
	border: 1px solid var(--clr-button-darkgreen);
	border-radius: 15px;
	height: .5rem;
	width: .5rem;
}

.bottomScreen-wrapper {
	margin-inline: auto;
	width: 13.125rem;
}
.buttonbottomPicture {
	background-color: var(--clr-button-darkgreen);
	border-radius: 50%;
	box-shadow: 2px 2px var(--clr-black);
	height: 1.625rem;
	width: 1.625rem;
}
.speakers {
	height: 1.5625rem;
	width: 4.6875rem;
}
div.sp {
	background-color: var(--clr-panel-darkgrey);
	border-radius: 30px;
	margin-bottom: .3125rem;
	height: .1875rem;
}

.bigbluebutton {
	background-color: var(--clr-button-darkgreen);
	border-radius: 50%;
	box-shadow: 2px 2px var(--clr-black);
	height: 3.125rem;
	width: 3.125rem;
	position: absolute;
	top: 395px;
	left: 30px;
}
.barbutton1,
.barbutton2 {
	border: 2px solid var(--clr-button-darkgreen);
	box-shadow: 1px 1px var(--clr-button-darkgreen);
	border-radius: 100px;
	height: .625rem;
	width: 3.125rem;
	position: absolute;
}
.barbutton1 {
	background-color: var(--clr-body);
	top: 405px;
	left: 100px;
}
.barbutton2 {
	background-color: var(--clr-button-lightblue-shadow);
	top: 405px;
	left: 165px;
}
.cross {
	width: 5.625rem;
	height: 5.625rem;
	position: absolute;
	top: 394px;
	left: 230px;
}

.topcross, 
.leftcross,
.midcross,
.rightcross,
.botcross {
	width: 30px;
	height: 30px;
	background-color: var(--clr-button-darkgreen);
}
.topcross {
	border-top-left-radius: 5px;
	border-top-right-radius: 5px;
	box-shadow: 3px 2px var(--clr-black);
	position: absolute;
	top: 0;
	left: 30px;
}
.leftcross {
	box-shadow: 3px 2px var(--clr-black);
	border-bottom-left-radius: 5px;
	border-top-left-radius: 5px;
	position: absolute;
	left: 0;
	top: 30px;
	z-index: 0;
}
.midcross {
	box-shadow: 3px 2px #010101;
	position: absolute;
	top: 30px;
	left: 30px;
}
.rightcross {
	border-bottom-right-radius: 5px;
	border-top-right-radius: 5px;
	box-shadow: 3px 2px #010101;
	position: absolute;
	top: 30px;
	right: 0;
	z-index: 1;
}
.botcross {
	border-bottom-left-radius: 5px;
	border-bottom-right-radius: 5px;
	box-shadow: 3px 2px #010101;
	position: absolute;
	bottom: 0;
	left: 30px;
}

.upT {
	border-left: 10px solid transparent;
	border-right: 10px solid transparent;
	border-bottom: 10px solid var(--clr-black);
	height: 0;
	width: 0;
	position: absolute;
	top: 5px;
	left: 4px;
}
.downT {
	border-left: 10px solid transparent;
	border-right: 10px solid transparent;
	border-top: 10px solid var(--clr-black);
	height: 0;
	width: 0;
	position: absolute;
	bottom: 5px;
	left: 4px;
}
.leftT {
	border-top: 10px solid transparent;
	border-right: 10px solid var(--clr-black);
	border-bottom: 10px solid transparent;
	height: 0;
	width: 0;
	position: absolute;
	top: 5px;
	left: 4px;
}
.rightT {
	border-top: 10px solid transparent;
	border-left: 10px solid var(--clr-black);
	border-bottom: 10px solid transparent;
	height: 0;
	width: 0;
	position: absolute;
	top: 5px;
	right: 5px;
}
.midCircle {
	background: radial-gradient(var(--clr-black), var(--clr-button-darkgreen));
	border-radius: 30px;
	height: 20px;
	width: 20px;
	position: absolute;
	top: 5px;
	left: 4px;
}

/* Right Panel */

.curve1_right {
	background-color: var(--clr-body);
	border-top-right-radius: 85px 60px;
	width: 10.375rem;
	height: 28.1875rem;
	position: absolute;
	bottom: 0;
	left: 0;
}

.bg_curve1_right {
	background-color: var(--clr-white);
	border-top-right-radius: 30px;
	height: 5rem;
	width: 21.875rem;
}
.curve2_right {
	background-color: var(--clr-white);
	border-bottom-left-radius: 85px 60px;
	height: 6.25rem;
	width: 13.5rem;
	position: absolute;
	top: 0;
	right: 0;
}
.bg_curve2_right {
	background-color: var(--clr-body);
	border-bottom-right-radius: 30px;
	box-shadow: 0px 9px var(--clr-body-shadow);
	height: 26.25rem;
	width: 21.875rem;
}

.stats {
	background-color: var(--clr-button-darkgreen);
	border-radius: 15px;
	box-shadow: 0 0 20px rgba(255, 255, 255, .2) inset;
	font-size: 1.375rem;
	height: 9.125rem;
	width: 17.5rem;
	padding: 10px;
	position: absolute;
	top: 130px;
	left: 25px;
	overflow-y: auto;
	overflow-x: hidden;
	z-index: 1;
}

/* Input Name */
.inputName__input {
	background-color: transparent;
	border: none;
	color: var(--clr-white);
}
.inputName__input:hover,
.inputName__input:focus {
	outline: none;
}

/* Movimientos, Habilidades */
.moves__horizontal-scroll,
.abilities__horizontal-scroll {
	display: flex;
	gap: .9375rem
}
.moves,
.abilities {
	background-color: var(--clr-button-darkgreen-tint);
	border-radius: 8px;
	padding: 10px;
	overflow-x: auto;
}
.moves {
	margin-bottom: .625rem;
}
.move,
.ability {
	flex: 1 0 auto;
}

.blueButtons {
	background-color: var(--clr-button-darkgreen);
	border-radius: 5px;
	display: grid;
	gap: 2px;
	position: absolute;
	top: 295px;
	left: 49px;
	z-index: 2;
}
.blueButtons1 {
	display: grid;
	grid-template-columns: repeat(5, 1fr);
	gap: 2px;
	position: relative;
	z-index: 1;
}
.blueButtons2 {
	display: grid;
	grid-template-columns: repeat(5, 1fr);
	gap: 2px;
	position: relative;
	z-index: 1;
}
div.blueButton {
	height: 2.1875rem;
	width: 2.8125rem;
	background-color: var(--clr-button-lightblue);
}
.blueButtons1 > div.blueButton:first-child {
	border-top-left-radius: 5px;
}
.blueButtons1 > div.blueButton:last-child {
	border-top-right-radius: 5px;
}
.blueButtons2 > div.blueButton:first-child {
	border-bottom-left-radius: 5px;
}
.blueButtons2 > div.blueButton:last-child {
	border-bottom-right-radius: 5px;
}

.barbutton3,
.barbutton4 {
    border: 2px solid var(--clr-button-darkgreen);
    border-radius: 100px;
    box-shadow: 1px 1px var(--clr-button-darkgreen);
	height: .625rem;
	width: 3.125rem;
	position: absolute;
	z-index: 1;
}
.barbutton3 {
	background-color: var(--clr-button-lightblue);
	top: 385px;
	left: 210px;
}
.barbutton4 {
    background-color: var(--clr-body);
	top: 385px;
	left: 270px;
}

.miniButtonGlass4,
.miniButtonGlass5 {
	border: 1px solid var(--clr-button-darkgreen);
	border-radius: 50%;
	width: .9375rem;
	height: .9375rem;
	position: absolute;
	z-index: 1;
}
.miniButtonGlass4 {
	background: var(--clr-button-yellow);
	top: 383px;
	left: 25px;
}
.miniButtonGlass5 {
	background: var(--clr-button-green);
	top: 383px;
	left: 51px;
}

.darkGreenBox1,
.darkGreenBox2 {
	background-color: var(--clr-button-darkgreen);
	border-radius: 15px;
	box-shadow: 2px 2px var(--clr-black);
	height: 4.375rem;
	width: 8.75rem;
	position: absolute;
	z-index: 1;
}
.darkGreenBox1 {
	top: 415px;
	left: 25px;
}

.darkGreenBox2 {
	top: 415px;
	left: 185px;
}
</style>