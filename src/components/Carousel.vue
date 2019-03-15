<template>
	<div>
		<p class="mt-4">
      Slides : {{ names.length }}<br />
    </p>
		<b-carousel 
      id="carousel"
      style="text-shadow: 1px 1px 2px #333;"
      controls
      indicators
      background="#ababab"
      :interval="4000"
      v-model="slide"
      @sliding-start="onSlideStart"
      @sliding-end="onSlideEnd"
    >
      <!-- Slides with custom text -->
      <b-carousel-slide v-for="name in names" class="client">	
        <ul>
        	<li><img v-bind:src="name.image" height="150" width="180" />
        	<li>Name : {{name.name}}</li>
        	<li class="feedback">Feedback : {{name.message}}</li>
        	<li><star-rating :show-rating="show_rating" :rating = "name.rating" read-only inactive-color="#BCBDBD"  
            active-color="#F7FB04" :glow="glow_value" glow-color="green"
            v-bind:star-size="35" class="rating" padding="1"></star-rating></li>
        	</li>
        </ul>
      </b-carousel-slide>
    </b-carousel>

	</div>
	
</template>
<script type="text/javascript">
	export default{
		name:'Carousel',

		data(){
			let names = this.$store.getters.CLIENTS
			console.log(names)
			return{
               names,
               slide:1,
               sliding:null,
               show_rating:false,
			}
		},
		methods: {
			onSlideStart(slide) {
        this.sliding = true
      },
      onSlideEnd(slide) {
        this.sliding = false
      },

		}
	}
</script>
<style scoped>
li{
	list-style-type: none;
	font-size: 18px;
	font-style: bold;
}
.client{
	height: 400px;
	text-align: center;
}
.rating{
	margin-left: 35%;
}
.display_rating{
	margin-left: 43%;
}
.feedback{
	clear:both;
	text-align: center;
}

</style>