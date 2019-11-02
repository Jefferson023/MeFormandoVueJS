<template>
  <b-card>
    <div slot="header">
      <b-row>
                <b-col md="11">
                    <h1>{{caption}}</h1>
                </b-col>
                <b-col md="1" v-if="comissaoPagina">
                    <b-button variant="link" style="margin-left:50%;margin-top:5%" to="/AdicionarFormando"><i class="icon-plus icons font-2xl"></i></b-button>
                </b-col>
            </b-row>
    </div>
    <b-table :dark="dark" :hover="hover" :striped="striped" :bordered="bordered" :small="small" :fixed="fixed" responsive="sm" :items="items" :fields="captions" :current-page="currentPage" :per-page="perPage" @row-clicked="rowClicked">
      <template slot="opcoes" >
        
        <b-button-group size="sm" class="mx-1"  v-if="comissao">
          <b-btn variant="primary" to="/EditarFormando">Edit</b-btn>
          <b-btn variant="danger">Remove</b-btn>
        </b-button-group>
      </template>
    </b-table>
    <nav>
      <b-pagination :total-rows="totalRows" :per-page="perPage" v-model="currentPage" prev-text="Prev" next-text="Next" hide-goto-end-buttons/>
    </nav>
    <b-button variant="primary" class="active mt-3" v-if="pagamento">Salvar</b-button>
  </b-card>
</template>

<script>


export default {
  name: 'c-table',
  inheritAttrs: false,
  
  props: {
    comissao:{
      type: Boolean,
      default: true
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
    }
  }
}
</script>
