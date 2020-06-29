<template>
	<transition name="slide">
		<div class="fixed h-full w-1/3 info-pane text-left p-8" v-show="this.infopane_show">
			<span class="close-it" @click="close_it()">X</span>
			<br />

			<h2 class="name">{{active_location.name}}</h2>
			<br />
			<b>Category:</b> {{active_location.category}}
			<br />
			<br />
			<div v-html="active_location.description" v-linkified ></div>
			<div id="google-data"></div>
		</div>
	</transition>
</template>

<script>
import Vue from 'vue'
import linkify from 'vue-linkify'
import axios from 'axios'

Vue.directive('linkified',linkify)




export default {
	created() {

		
		
		
	},
	async mounted() {



		this.$root.$on('show-location',data => {
        	this.reveal_location(data)
   		});
   			

		
	},
	data() {
		return {
			test: null,
			categories: ['Arts and Crafts','Books','Fashion and Beauty','Fitness','General Store','Home Decor','Restaurants','Wellness'],
			active_location: {name: 'test', description: 'test'},
			active_loc_ginfo: null,
			infopane_show: false
		}
	    
	},
	methods: {
		filtercategory: function(category) {
			//console.log(category)
			this.$root.$emit('filter-category',category)
		},
		reveal_location: function(location) {
			this.infopane_show = true;
			this.active_location = location;

			
			let nameURI = encodeURI(location.name);
			let latlng = location.lat + ',' + location.lng;
			


			axios.get('https://maps.googleapis.com/maps/api/place/findplacefromtext/json?input='+nameURI+'&inputtype=textquery&fields=photos,formatted_address,name,opening_hours,rating&locationbias=circle:1000@'+latlng+'&key='+process.env.GMAPS_KEY)
				.then(response => {

					console.log(response)

				});



		},
		close_it: function() {
			this.infopane_show = false
		}
	}
	
}

</script>



<style lang="scss">

.name {
	font-weight: 700;
	font-size: 1.25em;
}

.info-pane {
	background: white;
	z-index: 2000;
	top: 0;
	overflow: auto;
}

.slide-enter-active, .slide-leave-active {
  transition: all .5s;
}
.slide-enter, .slide-leave-to /* .fade-leave-active below version 2.1.8 */ {
  transform: translate(-100%, 0);
}

.close-it {
	position: absolute;
	right: .5em;
	top: 0em;
	font-family: arial;
	font-size: 2em;
	color: #ddd;
	cursor: pointer;
}


</style>
