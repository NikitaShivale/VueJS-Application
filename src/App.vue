<template>
<div class="container" id="app">
    
        <h1 class="text-primary;font-size:25px">Dog Gallery</h1> 
        <p style="font-size:18px">Select breed from  below</p>

        <select name="breedtype" v-on:change='getbreed($event)' class="form-control" @select = 'getbreed' :value='breed' v-model="selected">
            <option disabled value="">Please select one</option>
            <option v-for="b in breed" :key="b">{{b}}</option>
        </select>
      <p style="font-size:20px">Displaying Images for : {{selected}} breed</p>
      

<div class="row text-center" style="display:flex; flex-wrap:wrap" id="app">
        <div v-for="i in getimages" :key="i.id">
           <div class="col-lg-3 col-md-3 col-sm-6">
            <div class="thumbnail">   
                <img width="90%" :src="i">
            </div>
            </div>
         </div>
     </div>
    </div>
</template>

<script>
import axios from 'axios'

function buildurl (url){
    return 'https://dog.ceo/api/breed/' + url + '/images'
}
const breeds ="akita, norwegian, staffordshire, australian cardigan, scottish norwegian, lapphund, bichon, afghan basset, ibizan, plott, walker, bull, english, tibetan, bernese, swiss, caucasian, miniature, german,, germanlonghair, miniature, standard, toy,  chesapeake, curly, flatcoated, golden, rhodesian, giant,, miniature, english, gordon, irish, shetland, blenheim, brittany, cocker, irish, japanese, sussex, welsh, border, dandie, kerryblue, patterdale, russell, scottish, sealyham, westhighland, yorkshire"
    export default {
        
        name: '#App',
        data() {
            return {
                message: null,
                selected:'',
                breed: breeds.split(', '),
                b: 'hound'
            }
        },
        
        mounted() {
            this.getbreed('akita')    
        },
        methods: 
        {
             getbreed(breed) {
                this.$emit('selected')
                let url = buildurl(breed);

                axios.get(url).then((response) => {
                    this.message = response.data.message;
                }).catch(error => { console.log(error); });
            }
        },
        
        computed: {
            getimages (){
                return this.message;
            }
        }        
    }
</script>

<style lang="scss" scoped>
#app {
    font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    text-align: center;
    color: #2c3e50;
    background-color:lightcyan
}
h1{
    color:royalblue
}
</style>