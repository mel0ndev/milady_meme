<template>
	<v-app id="app">
		<div class="hider">
		<v-main>
			<div class="milady_background1"> 
				<v-img src="./assets/gifs/1.gif"
					height="25vh"
					width="25vh"
				> </v-img>
			</div>
			<div class="milady_background2">
				<v-img src="./assets/gifs/2.gif"
					height="15vh"
					width="15vh"
				> </v-img>
			</div>
			<div class="milady_background3"> 
				<v-img src="./assets/gifs/3.gif"
					height="25vh"
					width="25vh"
				> </v-img>
			</div>
      <v-container>
        <v-row>
          <v-col justify="center" align="center">
			  <v-sheet
				color="#F6E4D1"
				min-height="50vh"
				max-width="50vh"
				class="milady_sheet" 
			>
				<div class="milady_title">
					<h3> welcome to sams </h3>	
				</div>

				<div> 
					<p> redacted paragraph goes here </p>
				</div>
				<HelloWorld />
            </v-sheet>
		</v-col>
	</v-row>
	<v-row justify="center" align="center"> 
		<v-col justify="center" align="center">
			<v-sheet
				color="#F6E4D1"
				min-height="10vh"
				max-width="35vh"
				class="milady_subsheet" 
			>
			<div v-if="connected">
			<div class="account_class"> {{ account.substring(0, 5) + "..." + account.substring(14, 18) }} </div>
			<v-btn 
				plain 
				outlined 
				text 
				color="#ee90bf" 
				class="milady_button"
			> 
				mint 
			</v-btn>

		</div>

		<div v-else> <v-btn
				plain 
				outlined 
				text 
				color="#ee90bf" 
				class="milady_button"
				@click="connect"
			> 
				connect 
			</v-btn>
		</div>
	</v-sheet>

		</v-col>
	</v-row>

	<v-row>
		<v-col justify="center" align="center">
			<v-sheet
				color="#F6E4D1"
				min-height="25vh"
				max-width="50vh"
				class="milady_sheet" >
				<div class="milady_title">
					<h3> contact us </h3>	
				</div>
				<p> we are available for writings. please send us any comments you have in the form of mail. we will read everything </p>
				<v-img src="./assets/contact.jpeg"
					class="centered_img">
				</v-img>
				<p> <i> we love letters! </i> </p>
			</v-sheet>
		</v-col>
	</v-row>

	<v-row>
		<v-col justify="center" align="center">
			<v-btn color="black" icon> <v-icon> mdi-play </v-icon> </v-btn>
		</v-col>
	</v-row>
      </v-container>
  <div class="milady_background4"> 
	  <v-img src="./assets/gifs/4.gif"
					height="25vh"
					width="25vh"
				> </v-img>
  </div>
  <div class="milady_background5"> 
	  <v-img src="./assets/gifs/5.gif"
					height="15vh"
					width="15vh"
				> </v-img>
  </div>
  <div class="milady_background6"> 
	  <v-img src="./assets/text3.png"
					height="20vh"
					width="30vh"
				> </v-img>
  </div>
		<div class="milady_background7">
			<v-img src="./assets/text1.png"	
				height="10vh"
				width="25vh"
			>
			</v-img>
		</div>

		<div class="milady_background8">
			<v-img src="./assets/text5.png"	
				height="10vh"
				width="25vh"
			>
			</v-img>
		</div>

		<div class="milady_background9">
			<v-img src="./assets/saaaaaam.png"	
				height="10vh"
				width="15vh"
			>
			</v-img>
		</div>

		<div class="milady_background10">
			<v-img src="./assets/gifs/sams.gif"	
				height="30vh"
				width="30vh"
			>
			</v-img>
		</div>

		<div class="milady_background11">
			<v-img src="./assets/text2.png"	
				height="30vh"
				width="30vh"
			>
			</v-img>
		</div>

		<div class="milady_background12">
			<v-img src="./assets/text6.png"	
				height="30vh"
				width="30vh"
			>
			</v-img>
		</div>

		<div class="milady_background13">
			<v-img src="./assets/gifs/heart.gif"
				height="30vh"
				width="30vh"
			>
			</v-img>
		</div>

		<div class="creepy_text"> 
			<p> I am so glad you stopped by. This is my web page and it has things that I like. I also have pictures of my family. </p>
		</div>
  </v-main>
	<v-img src="./assets/infscroll.png"> </v-img>
  </div>
  </v-app>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue"; 
import { onMounted, ref} from "@vue/runtime-core"; 

export default {
	components: {
		HelloWorld, 
	},
	data() {
		return {
			connected: false,
			metamaskSupported: false,
			account: "",
		}	
	},
	methods: {
		async connect() {
			const account = await window.ethereum.request({method: "eth_requestAccounts"}); 
			if (account[0] !== 'undefined') {
				this.connected = true; 
				this.account = account[0]; 
				sessionStorage.setItem("account", this.account);
			}	
		}

	},
	mounted() {
		if (typeof window.ethereum !== 'undefined') {
			this.metamaskSupported  = true; 
		} else {
			console.log('metamask not supported'); 
		} 

		window.ethereum.on('accountsChanged', (accounts) => {
			// If user has locked/logout from MetaMask, this resets the accounts array to empty
			if (!accounts.length) {
				this.connected = false; 
				sessionStorage.removeItem("account"); 
			}
		});
		

		const account = sessionStorage.getItem("account"); 
		//for reload persistance	
		if (account != null) {
			this.connected = true; 
			console.log(account); 
		} else {
			this.connected = false; console.log(false); 
		}
	}
}
</script>

<script setup>
  //
</script>

<style> 

#app {
	background-image: url(./assets/background.gif); 
	background-size: 25rem; 
}

.hider {
	overflow: hidden; 
	position: relative; 
	height: 2500px; 
}

.account_class {
	color: black; 
}

.milady_sheet {
	border: 2px solid darkgray !important; 
}

.milady_subsheet {
	border: 2px solid darkgray !important; 
	padding-top: 2.5vh; 	
	padding-bottom: 2.5vh; 
}

.milady_title {
	border-bottom: 2px solid darkgray; 
	background-color: #013220; 
	color: white; 
}

.milady_button {
	text-decoration: none !important; 
	text-transform: none !important; 	
	border-radius: 0px !important; 
	width: 10rem; 
	height: 3rem !important;  
	font-size: 1.5rem !important;  
}

.milady_background1 {
	position: absolute; 
	top: 1vh; 
	left: 2vh; 
}

.milady_background2 {
	position: absolute; 
	top: 80vh;
	left: 50vh; 
}

.milady_background3 {
	position: absolute; 
	top: 60vh; 
	left: 5vh; 
}

.milady_background4 {
	position: absolute; 
	top: 15vh; 
	left: 130vh; 
}

.milady_background5 {
	position: absolute; 
	top: 60vh; 
	left: 130vh; 
}

.milady_background6 {
	position: absolute; 
	top: 5vh; 
	left: 125vh; 
}

.milady_background7 {
	position: absolute; 
	top: 40vh; 
	left: 5vh; 
}

.milady_background8 {
	position: absolute; 
	top: 10vh; 
	left: 40vh; 
}

.milady_background9 {
	position: absolute; 
	top: 50vh; 
	left: 50vh; 
}

.milady_background10 {
	position: absolute; 
	top: 20vh; 
	left: 30vh; 
}

.milady_background11 {
	position: absolute; 
	top: 40vh; 
	left: 150vh; 
}

.milady_background12 {
	position: absolute; 
	top: 70vh; 
	left: 160vh; 
}

.milady_background13 {
	position: absolute; 
	top: 5vh; 
	left: 160vh; 
}

.contain {
	display: flex;
	align: flex; 
	margin-right: 1px !important; 
	padding-left: 5REM !important;  
	width: 25REM !important; 
}

.centered_img {
	padding-top: 2rem; 
	padding-left: 5rem;
	padding-right: 5rem;
	width: 400px; 
}

.creepy_text {
	position: absolute; 
	top: 120vh; 
	left: 115vh; 
	color: white; 
	font-family: "Times New Roman"
}

.inf_scroll {
	
}


</style>

