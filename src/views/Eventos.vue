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

const someData = () => shuffleArray([
  {title: 'Samppa Nori',description: 'Samppa Nori'},
  {title: 'Estavan Lykos',description: 'Samppa Nori' },
  {title: 'Chetan Mohamed',description: 'Samppa Nori'},
  {title: 'Derick Maximinus',description: 'Samppa Nori'},
  {title: 'Friderik Dávid',description: 'Samppa Nori'},

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
        {key: 'description'}
      ],

      
    }
  }
}
</script>