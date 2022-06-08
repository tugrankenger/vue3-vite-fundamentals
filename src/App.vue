<template>
  <div>
    <!-- optiopns api ile composition api setup kullanilarak birlikte kullanilabilir. -->

    <h3>{{ title }}</h3>

    <input type="text" v-model="title"> <br><br>
    {{  titleLengthMessage }}

    <button @click="toggleIt">Show/hide</button><br><br>
    <p v-if="show">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Labore consectetur id odio harum voluptatum dolores optio ratione officiis obcaecati aut nam officia nesciunt cumque assumenda eius similique perspiciatis, eligendi quasi.</p>

    <button @click="counter --">-</button> &nbsp;
    <span>{{ counter }}</span> &nbsp;
    <button @click="counter ++">+</button> <br> <br> &nbsp;
    <span style="color:red" v-if="counter < 0">{{smallerThanZero}}</span>
    <span style="color:green" v-if="counter > 0">{{biggerThanZero}}</span>
  </div>
</template>

<script>
// reactive bir event icin {ref} import edilmeli(reactivite effect (ref) )
import {ref, computed} from "vue";
  export default{
    // data(){
    //   return{
    //     title: "this is a title",
    //   };
    // },
    // beforeCreate(){
    //   console.log("beforeCreate");
    // },
    // created(){
    //   console.log("created");
    // },

    setup(){ // setup fonksiyonu data, beforecreate, created metodlarinin yerine geldi.
              // yukaridaki beforecreate ve created metodlarindan once setup calisiyor.
              //  template asamasinda yani mount oldugunda beforecreate ve created calisir.
              // setup amaci data'daki reactivity henuz olusmadan once calismak ve data'yi ona gore olusturmak
              // setup fonksiyonu geriye bir obje return etmeli

      //console.log("setup")

      //const title = "this is a setup title" // burasi reactivite degil

      const title = ref("this is a setup title"); // simdi reactive oldu
      const show = ref(false);
      console.log(show);
      const counter = ref("0");
      const biggerThanZero = ref("Bigger than zero");
      const smallerThanZero = ref("Smaller than zero");

      const toggleIt = () =>{
        show.value = !show.value;
      } 

      //computed fonksiyon gibi calisan degiskenlerdir. kullanimi :

      const titleLengthMessage = computed(()=>{
        return title.value.length + " characters was writed";
      })

      return{
        toggleIt,
        biggerThanZero,
        smallerThanZero,
        counter,
        title,
        show,
        titleLengthMessage,
      }
    }
  }
</script>