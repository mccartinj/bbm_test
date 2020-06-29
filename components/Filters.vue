<template>

<div class="fixed h-full w-1/4 tray text-left p-8">
	<h2 class="text-left">Categories</h2>
	<ul class="category-list">
		<li v-for="category in categories" :key="category" class="mb-2">
			
			<label :for="category" class="flex items-center cursor-pointer">
				<div class="relative">
					<input type="checkbox" checked class="hidden" :id="category" @click="filtercategory(category)"/>
					<div class="toggle__line w-10 h-4 bg-gray-400 rounded-full shadow-inner"></div>
					<div class="toggle__dot absolute w-6 h-6 bg-white rounded-full shadow inset-y-0 left-0"></div>
				</div>
				<div class="ml-3 text-gray-700 font-medium" >{{ category }}</div>
			</label>
		</li>
	</ul>
</div>
	
</template>

<script>




export default {
	created() {
		
		
	},
	data() {
		return {
			test: null,
			categories: ['Books','Fashion and Beauty','Fitness','Home Decor','Restaurants','Wellness']
		}
	    
	},
	methods: {
		filtercategory: function(category) {
			//console.log(category)
			this.$root.$emit('filter-category',category)
		}
	}
	
}

</script>


<style lang="scss">

.tray {
	background: white;
	z-index: 2000;
	top: 0;
}

.toggle__dot {
  top: -.25rem;
  left: -.25rem;
  transition: all 0.3s ease-in-out;
}

input:checked ~ .toggle__dot {
  transform: translateX(100%);
  background-color: #48bb78;
}


</style>
