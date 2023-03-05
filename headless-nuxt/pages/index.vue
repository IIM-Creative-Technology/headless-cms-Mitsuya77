<template>
<div class="back">


    <nav>
        <div class="menu">	
            <div class="menu_links">
                <a href="http://localhost:3000/" class="link">HOME</a>
                <a href="" class="link">projects</a>
                <a href="" class="link">contacts</a>
            </div>
            <div class="menu_icon">
                <span class="icon"></span>
            </div>
        </div>
    </nav>

    <section class="wrapper">

        <div class="container">

            <div id="scene" class="scene" data-hover-only="false">


                <div class="circle" data-depth="1.2"></div>

                <div class="one" data-depth="0.9">
                    <div class="content">
                        <span class="piece"></span>
                        <span class="piece"></span>
                        <span class="piece"></span>
                    </div>
                </div>

                <div class="two" data-depth="0.60">
                    <div class="content">
                        <span class="piece"></span>
                        <span class="piece"></span>
                        <span class="piece"></span>
                    </div>
                </div>

                <div class="three" data-depth="0.40">
                    <div class="content">
                        <span class="piece"></span>
                        <span class="piece"></span>
                        <span class="piece"></span>
                    </div>
                </div>

                <p class="p404" data-depth="0.50">William</p>
                

            </div>

            <div class="text">
                <article>
                    <p>Chef de projet web. <br>IIM - Digital School Paris</p>
                    <button>En savoir plus !</button>
                </article>
            </div>

        </div>
    </section>

	

    <div class="projet">
        <h1 class="background"><span>Mes créations</span></h1>
		<div v-if="projet">
		<div v-if="types">
			<div class="text-filtre">
				Filter par projet : 
			</div>
			<div class="filterItem">	
				<button class="filter-btn" @click="filterProjet('all')">reset</button>
				<button class="filter-btn" v-for="type in types" @click="filterProjet(type)">
					{{ type }}
							
				</button>
			</div>
		</div>
		<div class="aaa">
			<div v-for="projet in filteredProjet" :key="projet.name" :projet="projet" >
            <nuxt-link :to="'/projects/' + projet.slug">
				<div class="projcard-container">
					<div class="projcard projcard-blue">
						<div class="projcard-innerbox">
							<div v-if="projet">
								<img class="projcard-img" :src="projet.image.url" />
								<div class="projcard-textbox">
									<div class="projcard-title"> {{projet.name}} </div>
								
									<div class="projcard-bar"></div>
									<div class="projcard-description"> {{projet.description}} </div>
									<h5>{{projet.projet_type.type}}</h5>
										<div class="projcard-tag">
											<div v-for="technologie in projet.technologies">
												<img :src="technologie.techno.url" alt="">
											</div>
										</div>
								</div>
							</div>
						</div>
					</div>
				</div>
			</nuxt-link>
		</div>
	</div>			
	
		</div>
           
    </div>

	
</div>			
</template>

<script setup>

const { find } = useStrapi()

const types = ref ([])
const projet = ref ()
const activeFilter = ref ('all')


const filterProjet = (type) => {
	activeFilter.value = type
}

const filteredProjet = computed(() => {
	if(activeFilter.value === 'all'){
		return projet.value.data
	}
	return projet.value.data.filter(projet => projet.projet_type.type === activeFilter.value)
})

onMounted(async () => {
	projet.value = await find('projets',{populate : 'deep'})
	types.value = new Set (projet.value.data.map(projet =>{
		return projet.projet_type.type
	}))
	console.log(projet.value)
})




// onMounted(async () =>{
const projets = await find('projets',{populate : 'deep'})
console.log(projets)
    // })
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css?family=Barlow+Condensed:300,400,500,600,700,800,900|Barlow:300,400,500,600,700,800,900&display=swap");

.back{
    background-color: rgba(0, 0, 0, 0.925);
    height: 100%;
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
    overflow-x: hidden;
}


* {
	 margin: 0;
	 padding: 0;
	 list-style: none;
	 border: 0;
	 -webkit-tap-highlight-color: transparent;
	 text-decoration: none;
	 color: inherit;
     font-family: "Barlow", sans-serif;
	 
}
h1 {
    font: 33px sans-serif;
    margin-top: 30px;
    text-align: center;
    text-transform: uppercase;
	color: white;
}
h5{
	padding-bottom: 15px;
}
.filter-btn	{
	
	margin-left: 50px;
}
.text-filtre{
	padding-top: 50px;
	padding-left: 50px;
	padding-bottom: 35px;
	color: white;
}
h1.background {
    position: relative;
    z-index: 1;
}
h1.background :before {
        border-top: 2px solid #dfdfdf;
        content:"";
        margin: 0 auto; 
        position: absolute; 
        top: 50%; left: 0; right: 0; bottom: 0;
        width: 95%;
        z-index: -1;
    }

    span { 
        
        background: #36184f;
        padding: 0 15px; 
    }
.filter-btn{
	background-color: #36184f;
	color: white;
	border: none;
	padding: 10px;
	border-radius: 5px;
}
.projet{
   padding-top: 500px;
}
 .logo {
	 position: fixed;
	 z-index: 5;
	 bottom: 10px;
	 right: 10px;
	 width: 40px;
	 height: 40px;
	 border-radius: 100%;
	 display: flex;
	 justify-content: center;
	 align-items: center;
	 background: rgba(0, 0, 0, 0.1);
	 border-radius: 100%;
	 backdrop-filter: blur(5px);
}
 .logo img {
	 width: 55%;
	 height: 55%;
	 transform: translateY(-1px);
	 opacity: 0.8;
}
 nav .menu {
	 width: 100%;
	 height: 80px;
	 position: absolute;
	 display: flex;
	 align-items: center;
	 justify-content: space-between;
	 padding: 0 5%;
	 box-sizing: border-box;
	 z-index: 3;
}
 nav .menu .website_name {
	 color: #695681;
	 font-weight: 600;
	 font-size: 20px;
	 letter-spacing: 1px;
	 background: white;
	 padding: 4px 8px;
	 border-radius: 2px;
	 opacity: 0.5;
	 transition: all 0.4s ease;
	 cursor: pointer;
}
 nav .menu .website_name:hover {
	 opacity: 1;
}
 nav .menu .menu_links {
	 transition: all 0.4s ease;
	 opacity: 0.5;
}
 nav .menu .menu_links:hover {
	 opacity: 1;
}
 @media screen and (max-width: 799px) {
	 nav .menu .menu_links {
		 display: none;
	}
}
 nav .menu .menu_links .link {
	 color: white;
	 text-transform: uppercase;
	 font-weight: 500;
	 margin-right: 50px;
	 letter-spacing: 2px;
	 position: relative;
	 transition: all 0.3s 0.2s ease;
}
 nav .menu .menu_links .link:last-child {
	 margin-right: 0;
}
 nav .menu .menu_links .link:before {
	 content: '';
	 position: absolute;
	 width: 0px;
	 height: 4px;
	 background: linear-gradient(90deg, #ffedc0 0%, #ff9d87 100%);
	 bottom: -10px;
	 border-radius: 4px;
	 transition: all 0.4s cubic-bezier(0.82, 0.02, 0.13, 1.26);
	 left: 100%;
}
 nav .menu .menu_links .link:hover {
	 opacity: 1;
	 color: #fb8a8a;
}
 nav .menu .menu_links .link:hover:before {
	 width: 40px;
	 left: 0;
}
 nav .menu .menu_icon {
	 width: 40px;
	 height: 40px;
	 position: relative;
	 display: none;
	 justify-content: center;
	 align-items: center;
	 cursor: pointer;
}
 @media screen and (max-width: 799px) {
	 nav .menu .menu_icon {
		 display: flex;
	}
}
 nav .menu .menu_icon .icon {
	 width: 24px;
	 height: 2px;
	 background: white;
	 position: absolute;
}
 nav .menu .menu_icon .icon:before, nav .menu .menu_icon .icon:after {
	 content: '';
	 width: 100%;
	 height: 100%;
	 background: inherit;
	 position: absolute;
	 transition: all 0.3s cubic-bezier(0.49, 0.04, 0, 1.55);
}
 nav .menu .menu_icon .icon:before {
	 transform: translateY(-8px);
}
 nav .menu .menu_icon .icon:after {
	 transform: translateY(8px);
}
 nav .menu .menu_icon:hover .icon {
	 background: #ffedc0;
}
 nav .menu .menu_icon:hover .icon:before {
	 transform: translateY(-10px);
}
 nav .menu .menu_icon:hover .icon:after {
	 transform: translateY(10px);
}
 .wrapper {
	 display: grid;
	 grid-template-columns: 1fr;
	 justify-content: center;
	 align-items: center;
	 height: 80vh;
	
}
 .wrapper .container {
	 margin: 0 auto;
	 transition: all 0.4s ease;
	 display: flex;
	 justify-content: center;
	 align-items: center;
	 position: relative;
}
 .wrapper .container .scene {
	 position: absolute;
	 width: 100vw;
	 height: 100vh;
	 vertical-align: middle;
}
 .wrapper .container .one, .wrapper .container , .wrapper .container .three, .wrapper .container .circle, .wrapper .container .p404 {
	 width: 60%;
	 height: 60%;
	 top: 20% !important;
	 left: 20% !important;
	 min-width: 400px;
	 min-height: 400px;
}
 .wrapper .container .one .content, .wrapper .container  .content, .wrapper .container .three .content, .wrapper .container .circle .content, .wrapper .container .p404 .content {
	 width: 600px;
	 height: 600px;
	 display: flex;
	 justify-content: center;
	 align-items: center;
	 position: absolute;
	 top: 50%;
	 left: 50%;
	 transform: translate(-50%, -50%);
	 animation: content 0.8s cubic-bezier(1, 0.06, 0.25, 1) backwards;
}
 @keyframes content {
	 0% {
		 width: 0;
	}
}
 .wrapper .container .one .content .piece, .wrapper .container .two .content .piece, .wrapper .container .three .content .piece, .wrapper .container .circle .content .piece, .wrapper .container .p404 .content .piece {
	 width: 200px;
	 height: 80px;
	 display: flex;
	 position: absolute;
	 border-radius: 80px;
	 z-index: 1;
	 animation: pieceLeft 8s cubic-bezier(1, 0.06, 0.25, 1) infinite both;
}
 @keyframes pieceLeft {
	 50% {
		 left: 80%;
		 width: 10%;
	}
}
 @keyframes pieceRight {
	 50% {
		 right: 80%;
		 width: 10%;
	}
}
 @media screen and (max-width: 799px) {
	 .wrapper .container .one, .wrapper .container , .wrapper .container .three, .wrapper .container .circle, .wrapper .container .p404 {
		 width: 90%;
		 height: 90%;
		 top: 5% !important;
		 left: 5% !important;
		 min-width: 280px;
		 min-height: 280px;
	}
}
 @media screen and (max-height: 660px) {
	 .wrapper .container .one, .wrapper .container .two, .wrapper .container .three, .wrapper .container .circle, .wrapper .container .p404 {
		 min-width: 280px;
		 min-height: 280px;
		 width: 60%;
		 height: 60%;
		 top: 20% !important;
		 left: 20% !important;
	}
}
 .wrapper .container .text {
	 width: 60%;
	 height: 40%;
	 min-width: 400px;
	 min-height: 500px;
	 position: absolute;
	 margin: 40px 0;
	 animation: text 0.6s 1.8s ease backwards;
}
 @keyframes text {
	 0% {
		 opacity: 0;
		 transform: translateY(40px);
	}
}
 @media screen and (max-width: 799px) {
	 .wrapper .container .text {
		 min-height: 400px;
		 height: 80%;
	}
}
 .wrapper .container .text article {
	 width: 400px;
	 position: absolute;
	 bottom: 0;
	 z-index: 4;
	 display: flex;
	 flex-direction: column;
	 justify-content: center;
	 align-items: center;
	 text-align: center;
	 bottom: 0;
	 left: 50%;
	 transform: translateX(-50%);
}
 @media screen and (max-width: 799px) {
	 .wrapper .container .text article {
		 width: 100%;
	}
}
 .wrapper .container .text article p {
	 color: white;
	 font-size: 18px;
	 letter-spacing: 0.6px;
	 margin-bottom: 40px;
	 text-shadow: 6px 6px 10px #32243e;
}
 .wrapper .container .text article button {
	 height: 40px;
	 padding: 0 30px;
	 border-radius: 50px;
	 cursor: pointer;
	 box-shadow: 0px 15px 20px rgba(54, 24, 79, 0.5);
	 z-index: 3;
	 color: #695681;
	 background-color: white;
	 text-transform: uppercase;
	 font-weight: 600;
	 font-size: 12px;
	 transition: all 0.3s ease;
}
 .wrapper .container .text article button:hover {
	 box-shadow: 0px 10px 10px -10px rgba(54, 24, 79, 0.5);
	 transform: translateY(5px);
	 background: #fb8a8a;
	 color: white;
}
 .wrapper .container .p404 {
	 font-size: 200px;
	 font-weight: 700;
	 letter-spacing: 4px;
	 color: white;
	 display: flex !important;
	 justify-content: center;
	 align-items: center;
	 position: absolute;
	 z-index: 2;
	 animation: anime404 0.6s cubic-bezier(0.3, 0.8, 1, 1.05) both;
	 animation-delay: 1.2s;
}
 @media screen and (max-width: 799px) {
	 .wrapper .container .p404 {
		 font-size: 100px;
	}
}
 @keyframes anime404 {
	 0% {
		 opacity: 0;
		 transform: scale(10) skew(20deg, 20deg);
	}
}
 .wrapper .container .p404:nth-of-type(2) {
	 color: #36184f;
	 z-index: 1;
	 animation-delay: 1s;
	 filter: blur(10px);
	 opacity: 0.8;
}
 .wrapper .container .circle {
	 position: absolute;
}
 .wrapper .container .circle:before {
	 content: '';
	 position: absolute;
	 width: 800px;
	 height: 800px;
	 background-color: rgba(54, 24, 79, 0.2);
	 border-radius: 100%;
	 top: 50%;
	 left: 50%;
	 transform: translate(-50%, -50%);
	 box-shadow: inset 5px 20px 40px rgba(54, 24, 79, 0.25), inset 5px 0px 5px rgba(50, 36, 62, 0.3), inset 5px 5px 20px rgba(50, 36, 62, 0.25), 2px 2px 5px rgba(255, 255, 255, 0.2);
	 animation: circle 0.8s cubic-bezier(1, 0.06, 0.25, 1) backwards;
}
 @keyframes circle {
	 0% {
		 width: 0;
		 height: 0;
	}
}
 @media screen and (max-width: 799px) {
	 .wrapper .container .circle:before {
		 width: 400px;
		 height: 400px;
	}
}
 .wrapper .container .one .content:before {
	 content: '';
	 position: absolute;
	 width: 600px;
	 height: 600px;
	 background-color: rgba(54, 24, 79, 0.3);
	 border-radius: 100%;
	 box-shadow: inset 5px 20px 40px rgba(54, 24, 79, 0.25), inset 5px 0px 5px rgba(50, 36, 62, 0.3), inset 5px 5px 20px rgba(50, 36, 62, 0.25), 2px 2px 5px rgba(255, 255, 255, 0.2);
	 animation: circle 0.8s 0.4s cubic-bezier(1, 0.06, 0.25, 1) backwards;
}
 @media screen and (max-width: 799px) {
	 .wrapper .container .one .content:before {
		 width: 300px;
		 height: 300px;
	}
}
 .wrapper .container .one .content .piece {
	 background: linear-gradient(90deg, #8077ea 13.7%, #eb73ff 94.65%);
}
 .wrapper .container .one .content .piece:nth-child(1) {
	 right: 15%;
	 top: 18%;
	 height: 30px;
	 width: 120px;
	 animation-delay: 0.5s;
	 animation-name: pieceRight;
}
 .wrapper .container .one .content .piece:nth-child(2) {
	 left: 15%;
	 top: 45%;
	 width: 150px;
	 height: 50px;
	 animation-delay: 1s;
	 animation-name: pieceLeft;
}
 .wrapper .container .one .content .piece:nth-child(3) {
	 left: 10%;
	 top: 75%;
	 height: 20px;
	 width: 70px;
	 animation-delay: 1.5s;
	 animation-name: pieceLeft;
}
 .wrapper .container .two .content .piece {
	 background: linear-gradient(90deg, #ffedc0 0%, #ff9d87 100%);
}
 .wrapper .container .two .content .piece:nth-child(1) {
	 left: 0%;
	 top: 25%;
	 height: 40px;
	 width: 120px;
	 animation-delay: 2s;
	 animation-name: pieceLeft;
}
 .wrapper .container .two .content .piece:nth-child(2) {
	 right: 15%;
	 top: 35%;
	 width: 180px;
	 height: 50px;
	 animation-delay: 2.5s;
	 animation-name: pieceRight;
}
 .wrapper .container .two .content .piece:nth-child(3) {
	 right: 10%;
	 top: 80%;
	 height: 20px;
	 width: 160px;
	 animation-delay: 3s;
	 animation-name: pieceRight;
}
 .wrapper .container .three .content .piece {
	 background: #fb8a8a;
}
 .wrapper .container .three .content .piece:nth-child(1) {
	 left: 25%;
	 top: 35%;
	 height: 20px;
	 width: 80px;
	 animation-name: pieceLeft;
	 animation-delay: 3.5s;
}
 .wrapper .container .three .content .piece:nth-child(2) {
	 right: 10%;
	 top: 55%;
	 width: 140px;
	 height: 40px;
	 animation-name: pieceRight;
	 animation-delay: 4s;
}
 .wrapper .container .three .content .piece:nth-child(3) {
	 left: 40%;
	 top: 68%;
	 height: 20px;
	 width: 80px;
	 animation-name: pieceLeft;
	 animation-delay: 4.5s;
}
 





.projcard-container {
	margin: 50px 0;
}

/* Actual Code: */
.projcard-container,
.projcard-container * {
	box-sizing: border-box;
}
.projcard-container {
	margin-left: auto;
	margin-right: auto;
	width: 1000px;
}
.projcard {
	position: relative;
	width: 100%;
	height: 300px;
	margin-bottom: 40px;
	border-radius: 10px;
	background-color: #fff;
	border: 2px solid #ddd;
	font-size: 18px;
	overflow: hidden;
	cursor: pointer;
	box-shadow: 0 4px 21px -12px rgba(0, 0, 0, .66);
	transition: box-shadow 0.2s ease, transform 0.2s ease;
}
.projcard:hover {
	box-shadow: 0 34px 32px -33px rgba(0, 0, 0, .18);
	transform: translate(0px, -3px);
}
.projcard::before {
	content: "";
	position: absolute;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	background-image: linear-gradient(-70deg, #424242, transparent 50%);
	opacity: 0.07;
}
.projcard:nth-child(2n)::before {
	background-image: linear-gradient(-250deg, #424242, transparent 50%);
}
.projcard-innerbox {
	position: absolute;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
}
.projcard-img {
	position: absolute;
	height: 300px;
	width: 400px;
	top: 0;
	left: 0;
	transition: transform 0.2s ease;
}
.projcard:nth-child(2n) .projcard-img {
	left: initial;
	right: 0;
}
.projcard:hover .projcard-img {
	transform: scale(1.05) rotate(1deg);
}
.projcard:hover .projcard-bar {
	width: 70px;
}
.projcard-textbox {
	position: absolute;
	top: 7%;
	bottom: 7%;
	left: 430px;
	width: calc(100% - 470px);
	font-size: 17px;
}
.projcard:nth-child(2n) .projcard-textbox {
	left: initial;
	right: 430px;
}
.projcard-textbox::before,
.projcard-textbox::after {
	content: "";
	position: absolute;
	display: block;
	background: #fff;
	top: -20%;
	left: -55px;
	height: 140%;
	width: 60px;
	transform: rotate(8deg);
}
.projcard:nth-child(2n) .projcard-textbox::before {
	display: none;
}
.projcard-textbox::after {
	display: none;
	left: initial;
	right: -55px;
}
.projcard:nth-child(2n) .projcard-textbox::after {
	display: block;
}
.projcard-textbox * {
	position: relative;
}
.projcard-title {
	
	font-size: 25px;
}

.projcard-bar {
	left: -2px;
	width: 50px;
	height: 5px;
	margin: 10px 0;
	border-radius: 5px;
	background-color: #fa1313;
	transition: width 0.2s ease;
}
.projcard-blue .projcard-bar { 
	background: linear-gradient(90deg, #ffedc0 0%, #ff9d87 100%); 
}

.projcard-description {
	z-index: 10;
	font-size: 15px;
	color: #424242;
	height: 125px;
	overflow: hidden;
	text-overflow: ellipsis;
}
.projcard-tagbox {
	position: absolute;
	bottom: 3%;
	font-size: 14px;
	cursor: default;
	user-select: none;
	pointer-events: none;
}
.projcard-tag {
	display: flex;
	gap: 15px;
	
}
.projcard-tag img{
	width: 50px;
	height: 50px;
}
</style>