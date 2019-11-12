<template>
  <b-card>
    <div slot="header" v-html="caption"></div>
   <b-table>
    </b-table>
    <b-table :dark="dark" :hover="hover" :striped="striped" :bordered="bordered" :small="small" :fixed="fixed" responsive="sm" :items="items" :fields="captions" :current-page="currentPage" :per-page="perPage" >
      <template slot="opcoes" slot-scope="item" >
        
        <b-button-group size="sm" class="mx-1">
          <b-btn variant="primary"  @click="rowClicked(item.item)">Aceitar</b-btn>
          <b-btn variant="danger">Recusar</b-btn>
        </b-button-group>
      </template>
    </b-table>
    <nav>
      
    </nav>
    
  </b-card>
</template>

<script>

import axios from "axios";
import qs from "qs";
export default {
  name: 'c-table',
  inheritAttrs: false,
  props: {
    caption: {
      type: String,
      default: 'Table'
    },
    hover: {
      type: Boolean,
      default: false
    },
    striped: {
      type: Boolean,
      default: false
    },
    bordered: {
      type: Boolean,
      default: false
    },
    small: {
      type: Boolean,
      default: false
    },
    fixed: {
      type: Boolean,
      default: false
    },
    tableData: {
      type: [Array, Function],
      default: () => []
    },
    fields: {
      type: [Array, Object],
      default: () => []
    },
    perPage: {
      type: Number,
      default: 20
    },
    dark: {
      type: Boolean,
      default: false
    }
  },
  data: () => {
    
    return {
      currentPage: 1,
    }
  },
  computed: {
    items: function() {
      const items =  this.tableData
      return Array.isArray(items)  ? items : items()
    },
    totalRows: function () { return this.getRowCount() },
    captions: function() { return this.fields }
  },
  methods: {
   
    getChecked(pago) {
      if(pago == true){
          return true
      }else{
         return  false
      }
            
    },
    getRowCount: function () {
      return this.items.length
    },
   rowClicked (item) {
       
      this.$emit('row-clicked', item)
      alert(item.id)
      const data = qs.stringify({
          id: item.id
        });
      axios
      .post(process.env.VUE_APP_API + "/usuario/aceitarConvite",data, {
        headers: {
          "content-type": "application/x-www-form-urlencoded;charset=utf-8",
          token: localStorage.getItem("user_token")
        }
      })
      .then(response => {
        if (response.status == 201) {
            alert("Deu certo!!!")
            this.$router.push('/')  
        } else {
            alert("Deu errado!!!")
        }
      })
      .catch(() => {
          alert("Deu certo(CATCH)!!!")
      });
    
      
    },
  }
}
</script>
