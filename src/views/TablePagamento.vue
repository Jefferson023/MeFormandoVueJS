<template>
  <b-card>
    <div slot="header">
      <b-row>
                <b-col md="11">
                    <h1>{{caption}}</h1>
                </b-col>
      </b-row>
    </div>
    <b-table>
    </b-table>
    <b-table :dark="dark" :hover="hover" :striped="striped" :bordered="bordered" :small="small" :fixed="fixed" responsive="sm" :items="items" :fields="captions" :current-page="currentPage" :per-page="perPage" >
      <template slot="opcoes" slot-scope="item" v-if="comissao" >
        
        <b-button-group size="sm" class="mx-1" >
          <b-btn variant="primary"  @click="rowClicked(item.item.email)">Edit</b-btn>
          <b-btn variant="danger">Remove</b-btn>
        </b-button-group>
      </template>
    </b-table>
  </b-card>
</template>

<script>

import axios from 'axios';
import qs from 'qs';
export default {
  name: 'c-table',
  inheritAttrs: false,
  
  props: {
    comissao:{
      type: Boolean,
      default: false
    },
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
    },
    comissaoPagina:{
      type :Boolean,
      default: true
    },
    comissao:{
      type :Boolean,
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
      const comissaoPagina = this.comissaoPagina
      return Array.isArray(items)  ? items : items()
    },
    totalRows: function () { return this.getRowCount() },
    captions: function() { return this.fields },
    
  },
  methods: {
    getBadge (status) {
      return status === 'pagamento' ? 'pagamento'
        : status === 'Inactive' ? 'secondary'
          : status === 'Pending' ? 'warning'
            : status === 'Banned' ? 'danger' : 'primary'
            
    },
    getRowCount: function () {
      return this.items.length
    },
    rowClicked (item) {
      this.$emit('row-clicked', item)
      alert(item)
      
    },

    editar(item){
      alert(item)
    }
  },
  created(){
    axios.get(process.env.VUE_APP_API + "/usuario/confirmadoComissao", {
        headers: {
          "content-type": "application/x-www-form-urlencoded;charset=utf-8",
          token: localStorage.getItem("user_token")
        }
      })
      .then(response => {
        if (response.data == true) {
          this.comissao = true;
        } else {
          this.comissao = false;
        }
      })
      .catch(() => {})
  },
}  
</script>
