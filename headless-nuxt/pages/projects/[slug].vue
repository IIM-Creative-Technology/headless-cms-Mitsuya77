<template>
    <div class="fond">  
        <nav>
        <div class="menu">
            <p class="website_name">LOGO</p>
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

        <div class="projcard-container">
					<div class="projcard projcard-blue">
						<div class="projcard-innerbox">
							<div v-if="projet">
								
								<div class="projcard-textbox">
									<div class="projcard-title"> {{projet.name}} </div>
								
									<div class="projcard-bar"></div>
									<div class="projcard-description"> {{projet.description}} </div>
                                    <img class="projcard-img" :src="projet.image.url" />
										<div class="projcard-tag">
                                            <p>{{projet.projet_type.type}}</p>
											<div v-for="technologie in projet.technologies">
												<img :src="technologie.techno.url" alt="">
											</div>
										</div>
								</div>
							</div>
						</div>
					</div>
		</div>
    </div>  
</template>

<script setup>

const { findOne } = useStrapi()
const route = useRoute()
const projet = ref()


onMounted ( async () => {
    projet.value = await findOne(`projets?filters[slug]=${route.params.slug}&populate=deep`)
    projet.value = projet.value.data[0]
    
})


</script>

<style scoped>
.fond {
    background-color: rgba(0, 0, 0, 0.925);
    height: 100%;
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
    
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

.projcard-container {
	margin: 50px 0;
}


.projcard-container,
.projcard-container * {
	box-sizing: border-box;
}
.projcard-container {
	margin-left: auto;
	margin-right: auto;
	width: 60%;
    padding-top: 65px;
}
.projcard {
	position: relative;
	width: 100%;
	height: 800px;
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
	height: 400px;
	width: 800px;
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
	left: 200px;
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
	
	font-size: 30px;
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
	font-size: 20px;
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
    justify-content: space-between;
	gap: 15px;
    padding-top: 60px;
	
}
.projcard-tag p{
    font-size: 20px;
    background-color: #8077ea;
    padding-top: 5px;
    padding-left: 5px;
    padding-right: 5px;
    padding-bottom: 5px;

}
.projcard-tag img{
	width: 50px;
	height: 50px;
}
</style>