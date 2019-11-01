<template>
  <div class="animated fadeIn">

    
    
    <b-row>
      <b-col lg="12">
        <votacao :table-data="items" :fields="fields" caption="<h1>   Votações</h1>">
          
        </votacao>


      </b-col>

 
    </b-row>

    
  </div>

</template>

<script>
import { shuffleArray } from '@/shared/utils'
import votacao from './Votacao.vue'

const someData = () => shuffleArray([
  {title: 'Titulo',description: 'Descricao'},
  {title: 'Estavan Lykos',description: 'Samppa Nori' },
  {title: 'Chetan Mohamed',description: 'Samppa Nori'},
  {title: 'Derick Maximinus',description: 'Samppa Nori'},
  {title: 'Friderik Dávid',description: 'Samppa Nori'},

])


export default {
  name: 'votacoes',
  components: {votacao},
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