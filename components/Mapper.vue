<template>
<div>
	<GMap
	      ref="gMap"
	      :center="{lat: 40.7128, lng: -74.0060}"
	      :options="{fullscreenControl: false, streetViewControl: true, mapTypeControl: false, zoomControl: true, gestureHandling: 'auto', styles: mapStyle}"
	      :zoom="12"
	      @loaded="resize_markers"
	>
		

		<GMapMarker
        v-for="location in locations"
        :key="location.id"
        :position="{lat: location.lat, lng: location.lng}"
        :options="{
        	'category': location.category, 
        	'name': location.Name,
        	'icon': {url: pins[location.category], origin: icon_origin, size: icon_size}

        }"  
        @click="show_location(location)"
        @filter-category="filter_marker"
        
      	>
      	<!--
      		<GMapInfoWindow :options="{maxWidth: 200}">
		      <code>
		        lat: {{ location.lat }},
		        lng: {{ location.lng }}
		      </code>
		    </GMapInfoWindow>
		-->

     	</GMapMarker>



	</GMap>

</div>
</template>
<!--//:options="{icon: location === currentLocation ? pins.selected : pins.notSelected}"-->

<script>
import axios from 'axios';


const mapstyles = [{"stylers":[{"visibility":"simplified"}]},{"featureType":"administrative.land_parcel","stylers":[{"visibility":"simplified"}]},{"featureType":"administrative.locality","stylers":[{"color":"#707070"}]},{"featureType":"administrative.neighborhood","elementType":"labels.text","stylers":[{"color":"#b15c8b"},{"visibility":"simplified"}]},{"featureType":"administrative.province","stylers":[{"visibility":"simplified"}]},{"featureType":"landscape.man_made","elementType":"geometry.fill","stylers":[{"color":"#ededed"},{"visibility":"off"}]},{"featureType":"landscape.natural","stylers":[{"visibility":"off"}]},{"featureType":"landscape.natural.landcover","stylers":[{"visibility":"off"}]},{"featureType":"landscape.natural.terrain","stylers":[{"visibility":"off"}]},{"featureType":"poi.attraction","stylers":[{"visibility":"off"}]},{"featureType":"poi.business","stylers":[{"visibility":"off"}]},{"featureType":"poi.medical","stylers":[{"visibility":"off"}]},{"featureType":"poi.park","stylers":[{"visibility":"simplified"}]},{"featureType":"poi.park","elementType":"geometry.fill","stylers":[{"color":"#b9e899"}]},{"featureType":"poi.park","elementType":"labels.icon","stylers":[{"visibility":"off"}]},{"featureType":"poi.park","elementType":"labels.text","stylers":[{"color":"#2da64b"}]},{"featureType":"poi.place_of_worship","stylers":[{"visibility":"simplified"}]},{"featureType":"poi.school","stylers":[{"visibility":"simplified"}]},{"featureType":"poi.sports_complex","stylers":[{"visibility":"off"}]},{"featureType":"road","stylers":[{"visibility":"simplified"}]},{"featureType":"road","elementType":"labels.text","stylers":[{"lightness":10}]},{"featureType":"road.highway","elementType":"geometry.fill","stylers":[{"color":"#e8c1d6"},{"lightness":30}]},{"featureType":"road.highway","elementType":"labels.icon","stylers":[{"visibility":"off"}]},{"featureType":"transit.line","stylers":[{"visibility":"simplified"}]},{"featureType":"transit.station","elementType":"labels.icon","stylers":[{"visibility":"simplified"}]},{"featureType":"transit.station.airport","stylers":[{"visibility":"simplified"}]},{"featureType":"transit.station.airport","elementType":"labels.icon","stylers":[{"visibility":"off"}]},{"featureType":"transit.station.bus","stylers":[{"visibility":"simplified"}]},{"featureType":"transit.station.rail","elementType":"labels.icon","stylers":[{"lightness":5}]},{"featureType":"transit.station.rail","elementType":"labels.text","stylers":[{"color":"#045e8c"},{"visibility":"simplified"}]},{"featureType":"water","elementType":"geometry.fill","stylers":[{"color":"#29b7f2"},{"lightness":60}]},{"featureType":"water","elementType":"labels.icon","stylers":[{"color":"#045e8c"}]},{"featureType":"water","elementType":"labels.text.fill","stylers":[{"color":"#045e8c"}]}];

let dataset = {}

export default {
	created() {
		axios.get('/data/bob2020.geojson')
			.then(response => {
				
				//this.locations = response.data

				let feature_collection = response.data;
				let features = feature_collection.features;
				let businesses = []
				

				features.forEach(feature => {
					//console.log(feature)

					let business =  {}
					
					business.name = feature.properties.Name
					business.category = feature.properties.category
					business.description = feature.properties.description;

					if(feature.geometry == null) {

					} else {
						business.lat = feature["geometry"]["coordinates"][1];
						business.lng = feature["geometry"]["coordinates"][0];
					}

					
					business.properties = feature.properties;
					//console.log(business);
					
					businesses.push(business);
					

				});

				
				//console.log(businesses)
				
				this.locations = businesses;
				

			})
			.catch(e => {
				//this.errors.push(e)
				console.log('error');
				console.log(e);
			})

			
		
	},
	async mounted() {

		this.$root.$on('filter-category',data => {
        	this.filter_marker(data)
   		});
   			

		
	},
	data() {
	    return {
	      currentLocation: {},
	      locationsVisibleOnMap: "",
	      locations: this.locations,
	      pins: {
	      	'Arts and Crafts': '/icons/Arts and Crafts.png',
	      	'Books': '/icons/Books.png',
	      	'Fashion and Beauty': '/icons/Fashion and Beauty.png',
	      	'Fitness': '/icons/Fitness.png',
	      	'General Store': '/icons/General Store.png',
	      	'Home Decor': '/icons/Home Decor.png',
	      	'Restaurants': '/icons/Restaurants.png',
	      	'Wellness': '/icons/Wellness.png',
	      },
	      clusterStyle: [  ],
	      mapStyle: mapstyles,
	      icon_size: null,
	      icon_origin: null
	    };
	},
	methods: {
		filter_marker(category) {
			//console.log('from filter-marker: '+category);
			//console.log(this.$refs.gMap);

			//console.log('main: '+category);
			let markers = this.$refs.gMap.markers;
			
			markers.forEach(marker => {
				
				//console.log(marker.category);


				if (category == marker.category) {
					//console.log(marker)
					if (marker.getVisible() == false) {
						marker.setVisible(true)
					} else {
						marker.setVisible(false)
					}
					
				}
			})
		},

		resize_markers() {
			
			//this.icon_size = new this.$refs.gMap.google.maps.Size(30,30);
	   		//this.icon_origin = new this.$refs.gMap.google.maps.Point(0, 0);
		},

		show_location(location) {
			
		
			this.$root.$emit('show-location',location)

		}
	}
	
}

</script>


<style lang="scss">

.GMap {
	width: 100%;
	height: 100%;
	position: absolute;
	top: 0;
	bottom: 0;
}

.GMap__Wrapper {
	width: 100%;
	height: 100%;	
}

</style>
