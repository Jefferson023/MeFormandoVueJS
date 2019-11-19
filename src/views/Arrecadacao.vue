<template >
    <b-card>
        <div slot="header">
            <b-row>
                <b-col md="11">
                    <h1>{{caption}}</h1>
                </b-col>
                <b-col md="1">
                    <b-button variant="link" style="margin-left:50%;margin-top:5%" to="/AdicionarArrecadacao"><i class="icon-plus icons font-2xl" v-if="comissao"></i></b-button>
                </b-col>
            </b-row>
        </div>
    

    <b-list-group :items="items" :current-page="currentPage" :per-page="perPage" @row-clicked="rowClicked">
        <b-list-group-item  v-for="item in items" v-bind:key="item" @click="rowClicked(item)" class="flex-column align-items-start"  >
            <h5>
            {{ item.titulo }} 
            </h5>
            <p>
                {{ item.dateInicial }} / {{ item.dateFinal }}
            </p>
        </b-list-group-item >
        
    </b-list-group>
        
    </b-card>
</template>

<script>
import { type } from 'os'
import axios from "axios";
import qs from "qs";
export default {
    
    name: 'arrecadacao',
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
        comissao:{
            type:Boolean,
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
        
    },
    methods: {
    
        getRowCount: function () {
        return this.items.length
        },
        rowClicked (item) {
           this.$emit('row-clicked', item)
           this.$router.push({name:'Arrecadacao Selecionada',params:{Pid:item.id}})
           
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
      .catch(() => {});
      
    }
}

   


</script>

