<template>
  <b-card>
    <div slot="header" v-html="caption"></div>
    <b-table :dark="dark" :hover="hover" :striped="striped" :bordered="bordered" :small="small" :fixed="fixed" responsive="sm" :items="items" :fields="captions" :current-page="currentPage" :per-page="perPage" @row-clicked="rowClicked">
      <template slot="pago" slot-scope="data">
        <!-- <b-badge :variant="getBadge(data.item.status)">{{data.item.status}}</b-badge> -->
         <input type="checkbox" :checked="getChecked(data.item.pago)" class="form-check-input" id="exampleCheck1">
         


      </template>
    </b-table>
    <nav>
      <b-button class="d-sm-down-none" variant="success">Salvar</b-button>
    </nav>
    
  </b-card>
</template>

<script>


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
    }
  }
}
</script>
