<template >
    <b-card>
        <div slot="header">
            <b-row>
                <b-col md="11">
                    <h1>{{caption}}</h1>
                </b-col>
                <b-col md="1">
                    <b-button variant="link" style="margin-left:50%;margin-top:5%" to="/AdicionarEvento"><i class="icon-plus icons font-2xl"></i></b-button>
                </b-col>
            </b-row>
        </div>
    

    <b-list-group :items="items" :current-page="currentPage" :per-page="perPage" @row-clicked="rowClicked">
        <b-list-group-item  v-for="item in items" v-bind:key="item" @click="rowClicked(item)" class="flex-column align-items-start"  >
            <h5>
            {{ item.title }} - {{item.date}}
            </h5>
            <p>
                {{ item.description }}
            </p>
        </b-list-group-item >
        
    </b-list-group>
        
    </b-card>
</template>

<script>
export default {
    
    name: 'evento',
    inheritAttrs: false, 
    props: {
       caption: {
            type: String,
            default: 'list-group '
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
        
    },
    methods: {
    
        getRowCount: function () {
        return this.items.length
        },
        rowClicked (item) {
           this.$emit('row-clicked', item)
           this.$router.push({name:'Evento Selecionado',params:{Pid:item.title}})
           
        }

        
    }
}

   


</script>

