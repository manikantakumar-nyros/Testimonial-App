<template>
	<div>
    <div class="form">
		<h1>VueJS Feedback Form</h1>
		<b-form @submit.prevent="onSubmit">    
		    <label>Name:</label>
          <b-form-input placeholder="Name" type="text" v-model="name" :class="{ red_color: name_err }" /><br/>
          <label>Photo:</label>
          <img src="previewImage" class="uploading-image" />
          <b-form-file accept="image/*" @change="uploadImage" id="file-input" /><br/><br/>
          <label>Feedback:</label>
          <b-form-textarea placeholder="Please Enter your feedback" v-model="message" rows="3" max-rows="6" :class="{ red_color: msg_err }" /><br/>
          <label>Rating:</label>
          <b-form-select placeholder="Rating" v-model="selected" :class="{ red_color: rating_err }">
          <option v-for="option in options" :value="option.value">
                    {{ option.number }}
             </option>
          </b-form-select><br/><br/>
          <b-button type="submit">submit</b-button><br/>
      </b-form>
    </div>
	</div>
</template>

<script>
export default {
  name: 'TestimonialForm',
data(){
	return{
		name:"",
		name_err:false,
		client_name:"",
		message:"",
		client_msg:"",
		msg_err:false,
		selected:"5",
		options:[
			{number:"1", value:"1"},
			{number:"2", value:"2"},
			{number:"3", value:"3"},
			{number:"4", value:"4"},
			{number:"5", value:"5"},
		],
		rating_err:false,
		client_rating:"",
    previewImage:null,
	}
},
methods:{
	onSubmit () {
      if(!this.name){
        this.name_err = true;
      } else {
        this.name_err = false;
      }
      
      if(!this.message){
      	this.msg_err = true;
      } else {
      	this.msg_err = false;
      }
      if(!this.selected){
      	this.rating_err = true;
      } else {
      	this.rating_err = false;
      }
      
      if (this.name && this.message && this.selected && this.previewImage) {
      	let data = { 
      		name: this.name, 
      		message: this.message, 
      		rating: this.selected,
          image: this.previewImage, 
      	}
        console.log(this.image)
      	this.$store.dispatch('SAVE_CLIENT', data)
      }
      this.name=this.message=this.selected=this.previewImage="";
  },
  uploadImage(e){
                const image = e.target.files[0];
                const reader = new FileReader();
                reader.readAsDataURL(image);
                reader.onload = e =>{
                    this.previewImage = e.target.result;
                    console.log(this.previewImage);
                };

  }
}
}     
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.red_color {
  border-color: red;
  box-shadow: 0px 0px 6px 0px red;
}
button{
  background-color: #FF5733;
  border-radius: 7px;
  border-color: none;
  padding:5px;
}
img{
  display:none;
}
.form{
  background-color:olive;
  padding-right:10px;
  padding-left: 10px;
  margin-left: 30%;
  margin-right: 30%;
  border-radius:7px;
}
</style>