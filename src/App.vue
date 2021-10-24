<template>
  <div id="app"> 
<div>
  <b-navbar variant="danger" type="light" class="d-flex justify-content-center align-items-center">
    
    <b-navbar-brand href="#">Spor Ayakkabı</b-navbar-brand>
        <b-dropdown id="dropdown-right" right text="Sepet" variant="outline-danger" class="m-2">
          <template #button-content>
             &#128722;<span class="right"></span>
             <b-badge variant="light">{{basketAllItemCount}}</b-badge>
          </template>
          
          <b-dropdown-item v-show="basket.length===0">        
          Sepetiniz Boş
        </b-dropdown-item>
        
       <b-dropdown-item v-for="(el,i) in basket" :key="i" href="#">
         <div class="d-flex align-items-center"><b-col>
                      <img height="100" width="100" :src="el.image" class="cart-img rounded-3"/>
                    </b-col><b-button class="mx-2" @click="productCal({value: el,type:'-'})" variant="dark" size="sm">-</b-button>
         {{1}}
         <b-button class="mx-2" @click="productCal({value: el,type:'+'})" variant="success" size="sm">+</b-button>
         <b-button @click="productCal({value: el,type:'del'})" variant="danger" size="sm">x</b-button>
         {{el.title}} - Ara Toplam: {{(el.price * el.count).toFixed(2)}} $</div>
         
       </b-dropdown-item> 
          
         
  </b-dropdown> 
  </b-navbar> 

</div>
        
   <b-row class="d-flex justify-content-around">
      <shoe-card v-for="(el,i) in shoeInfoList " 
      :key="i" 
      :info="el"
      @addShoe="productCal({value:$event,type: 'add'})"      
      />
      </b-row>
  </div>
</template>

<script>
import ShoeCard from './components/ShoeCard.vue'


export default {
  name: 'App',
  components: {    
    ShoeCard
  },
  data(){
    return{
      shoeInfoList:[
        {
           category: "WOMEN",
           title: "Nike React Infinity Run Flyknit ",
           price: 130,
           summary:
            "Kadın Koşu Yol Ayakkabısı",
           rating: 3,
           color: "Pink",
           sizes: [35, 36, 37, 38, 39, 40],           
           image:require('@/assets/pinkshoes.jpg'),

        },
        {
           category: "WOMEN",
           title: "Nike React Infinity Run Flyknit 2",
           price: 155,
           summary:
            "Kadın Koşu Yol Ayakkabısı",
           rating: 4,
           color: "Pink",
           sizes: [35, 36, 37, 38, 39, 40],           
           image:require('@/assets/pink2.png'),

        },
        {
           category: "MEN",
           title: "Nike React Infinity Run Flyknit 2 You",
           price: 185,
           summary:
            "Erkek Koşu Yol Ayakkabısı",
           rating: 5,
           color: "Blue",
           sizes: [35, 36, 37, 38, 39, 40],           
           image:require('@/assets/blueshoes.png'),

        },
        {
           category: "MEN",
           title: "Nike React Infinity Run Flyknit 2 By You",
           price: 170,
           summary:
            "Erkek Koşu Yol Ayakkabısı",
           rating: 5,
           color: "Blue",
           sizes: [35, 36, 37, 38, 39, 40],           
           image:require('@/assets/blue2.png'),

        },
  
      ],
      basket: []
   }
  } ,
    computed:{
      basketAllItemCount(){ 
      let count=0
      for(let i=0;i<this.basket.length;i++){
      count+=this.basket[i].count
      }
      return count
      },
      totalPrice(){
      let totalPrice=0
       for(let i=0;i<this.basket.length;i++){
      totalPrice += this.basket[i].price
      }      
      return totalPrice
      }
    },
          
    

    
    methods: {

    productCal(val){
         let index = this.basket.findIndex(el=>el.title===val.value.title)

      switch(val.type){
          case 'add':
            if(index>=0){
              this.basket[index].count++
            } else{
          this.basket.unshift({...val.value,count: 1})
            }
              break;
          case '+':
            this.basket[index].count++
              break;
          case '-':
            if(this.basket[index].count>1){           
              this.basket[index].count--
            }else{
              this.basket.splice(index,1)
         }
              break;
          case 'del':
              this.basket.splice(index,1)
              break;
      default:
      }
    }
   }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
