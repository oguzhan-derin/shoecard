<template>
  <div>
    <b-card
        v-bind:title="info.title"
        img :src="info.image"
        img-alt="Image"
        img-top
        tag="article"
        style="width: 20rem;"
        class="mb-2" >

        <b-card-img  height="225" width="200" :src="info.image" alt="Image" class="rounded-3 ml-2">

        </b-card-img>
      
        <b-card-text>{{info.summary}}</b-card-text>

      
        <b-row class="justify-content-around">
            <div class="d-flex flex-row align-items-center justify-center">
                <span v-for="(el,i) in info.rating" 
                       :key="i" 
                       class="fa fa-star checked" />
                <span  v-for="(el,i) in (5-info.rating)" 
                       :key="'empty'+i" 
                       class="fa fa-star" />
             </div>
                    <b-row class=mt-1>
                    <b-card-text class="text-left product-price">
                        $ {{info.price}}</b-card-text>
                  </b-row>
    <button @click="addShoe(info)" type="button" class="btn btn-success">Add To Card
      <span class="badge badge-light"></span>
    </button>
   </b-row>
  </b-card>
 </div>
</template>

<script>
export default {
    name:'ShoeCard',
    props:{
        info: Object
    },
    data(){
        return{
         sizes:this.info.sizes[0],
         comPutedPrice:this.info.price
        }
    },
    computed:{
    changePrice(){
      return this.info.price + this.info.price * (this.info.sizes)
    }
    },

    methods: {
        addShoe(val){
            
            this.$emit('addShoe',val),

            this.$bvToast.toast(`Ürün Sepete Eklendi`, {
            title: 'Ürün Eklendi!',
            autoHideDelay: 2000,
            appendToast: true,
            toaster: 'b-toaster-top-right'
        })

        },
      changeSizes(val){
        this.sizes=val
      }
}
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.checked {
  color: orange;
}
</style>