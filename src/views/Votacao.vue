<template >
    <b-card>
        <div slot="header" v-html="caption"></div>
    

    <b-list-group :items="items" :current-page="currentPage" :per-page="perPage" @row-clicked="rowClicked">
        <b-list-group-item  v-for="item in items" v-bind:key="item" to="/voto" class="flex-column align-items-start"  >
            <h5>
            {{ item.title }}
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
    name: 'votacao',
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
        }
    }
}

   


</script>

