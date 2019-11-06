<template>
  <div class="animated fadeIn">

    
    
    <b-row>
      <b-col lg="12">
        <evento :table-data="items" :fields="fields" caption="Eventos">
          
        </evento>


      </b-col>

 
    </b-row>

    
  </div>

</template>

<script>
import { shuffleArray } from '@/shared/utils'
import evento from './Evento.vue'
import axios from 'axios';
import qs from 'qs';
const someData = () => shuffleArray([
  {title: 'Aula da Saudade',description: 'Samppa Nori',date: '20/06/2019'},
  {title: 'Missa',description: 'Samppa Nori', date: '20/05/2019'},
  {title: 'Colação de grau',description: 'Samppa Nori',date: '20/04/2019'},
  {title: 'Festa de Formatura',description: 'Samppa Nori',date: '20/03/2019'},
  {title: 'Fotos',description: 'Samppa Nori',date: '20/02/2019'},

])


export default {
  
  name: 'eventos',
  components: {evento},
  data: () => {
    return {
      items: someData,
      itemsArray: someData(),
      fields: [
        {key: 'title'},
        {key: 'description'},
        {key: 'date'}
      ],

      
    }
  },
  created()  {
        
        const header = {'content-type': 'application/x-www-form-urlencoded;charset=utf-8',token: localStorage.getItem('user_token')}
        axios.get(process.env.VUE_APP_API+"/evento/eventos", header).then((response) =>{
            if(response.data == null){
              alert("Null!!!")
            }else{
              for( item in response.data){
                alert(item)
              }
            }
            console.log(response.data)
            
        }).catch(()=>{
            alert("Erro catch")
        })
    }
}
</script>